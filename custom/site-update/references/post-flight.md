# Phases 5–7: Post-Flight Verification, Rollback Decisions & Cleanup

---

## Phase 5: Post-Flight Verification

The goal is to compare the current site state against the pre-flight baseline and detect any regressions caused by the updates.

### Step 5.1: Site Health Check

Run `mcm/site-health` and compare against the Phase 0 baseline:

| Check | Pre-flight | Post-flight | Status |
|-------|-----------|-------------|--------|
| Fatal errors | [baseline] | [current] | OK / NEW ERROR |
| Paused plugins | [baseline] | [current] | OK / NEW PAUSE |
| Memory usage | [baseline] | [current] | OK / INCREASED |

**Red flags that require immediate attention:**
- Any NEW fatal error that wasn't in the pre-flight baseline
- Any plugin that is now paused (was active before)
- Significant memory increase (>50% more than baseline)

### Step 5.2: Error Log Review

Run `mcm/error-log` with `lines: 50` and filter for entries AFTER the pre-flight baseline timestamp.

**What to look for:**
- **Fatal errors** (PHP Fatal error) → immediate rollback candidate
- **Deprecated notices** from updated plugins → inform user, usually non-critical
- **Warning messages** related to updated items → flag for user review
- **Database errors** → serious, may indicate compatibility issue

Classify each new log entry:

```
NEW LOG ENTRIES SINCE UPDATE:
─────────────────────────────
[🔴 CRITICAL] Fatal error in updated-plugin.php line 234 — ROLLBACK RECOMMENDED
[🟡 WARNING]  Deprecated function in theme-functions.php — monitor
[🟢 NOTICE]   Minor notice in translation loading — safe to ignore
```

### Step 5.3: Page Visual Verification

Visit the **same pages** checked in Phase 0, in the same order.

**If browser capabilities are available:**

1. Navigate to each pre-flight URL
2. Take a screenshot
3. Compare against the pre-flight state:
   - Does the page load completely?
   - Is the layout intact (no broken CSS/JS)?
   - Are all key elements present?
   - Are there any new PHP errors or warnings visible?
   - Do forms/interactive elements appear functional?

**If browser capabilities are NOT available:**

1. Rely on `mcm/site-health` results from Step 5.1
2. Check `mcm/error-log` for any 404 or rendering errors
3. Use `mcm/system-info` with `sections: ["plugins", "theme"]` to verify all plugins are active and theme is intact

### Step 5.4: Regression Classification

Based on all post-flight checks, classify the overall result:

**✅ ALL CLEAR** — No new errors, pages look identical to pre-flight, no new log entries
- Proceed to Phase 7 (cleanup)

**🟡 MINOR ISSUES** — Deprecation notices or non-fatal warnings, pages look fine
- Inform the user of the warnings
- Recommend monitoring but no rollback needed
- Proceed to Phase 7

**🔴 REGRESSION DETECTED** — New fatal errors, broken pages, or paused plugins
- Proceed to Phase 6 immediately for rollback decisions

---

## Phase 6: Rollback Decision

This phase is only needed if Phase 5 detected regressions.

### Step 6.1: Identify the Culprit

If multiple items were updated, determine which update caused the issue:

1. Check the error log — fatal errors usually name the file/plugin responsible
2. Check paused plugins — WordPress auto-pauses plugins that cause fatal errors
3. If unclear, the last updated item is the most likely culprit

### Step 6.2: Rollback Procedure

For the identified problematic item:

1. **List available snapshots**: `mcm/list-snapshots` filtered by the item's slug
2. **Confirm with user**: "Plugin X caused a fatal error after updating to version Y. I recommend rolling back to version Z (snapshot from [timestamp]). Should I proceed?"
3. **Execute rollback**: `mcm/restore-snapshot` with the snapshot ID

**IMPORTANT:** `mcm/restore-snapshot` automatically creates a safety snapshot of the current (broken) state before restoring. This means you can undo the rollback if needed.

4. **Verify the rollback**: Run `mcm/site-health` to confirm the fatal error is gone
5. **Re-check pages**: Visit the same pages to confirm the site is functional again

### Step 6.3: Partial Rollback Strategy

If multiple plugins were updated and only one caused issues:

- Roll back ONLY the problematic item
- Keep the other successful updates in place
- Re-verify after the rollback to ensure the combination is stable

### Step 6.4: Full Rollback

If the site is in a critical state and the culprit is unclear:

- Roll back ALL updated items using their snapshots, in reverse order
- Start with the last updated item and work backwards
- Verify after each rollback until the site is stable
- Report which rollback fixed the issue

---

## Phase 7: Cleanup & Final Report

This phase is MANDATORY regardless of whether updates succeeded or failed.

### Step 7.1: Maintenance Mode Check

**This is the most critical cleanup step.** WordPress creates a `.maintenance` file in the site root during updates. If it's left behind, the entire site shows "Briefly unavailable for scheduled maintenance" to all visitors.

**Check procedure:**

1. **If browser is available:** Navigate to the site's homepage. If you see the maintenance message, the file needs to be removed.

2. **Always verify programmatically:**
   - Run `mcm/delete-maintenance` — this ability checks if the `.maintenance` file exists and deletes it
   - If the file was found and deleted, inform the user
   - If the file was not found, no action needed

3. **After removal:** Visit the homepage again to confirm the site is accessible.

**This check must happen even if:**
- All updates succeeded without errors
- No updates were actually performed (dry run)
- The session is ending for any reason

### Step 7.2: Cache Clearing

After updates, cached content may show old versions of CSS/JS or pages:

1. Run `mcm/flush-cache` to clear the application cache (Redis/Memcached/object cache)
2. Optionally, if the user agrees, run `mcm/clear-cache` to empty all cache directories

**Note:** `mcm/clear-cache` is destructive and requires user confirmation. For routine updates, `mcm/flush-cache` is usually sufficient.

### Step 7.3: Final Status Report

Present a clear summary to the user:

```
═══════════════════════════════════════
  MAINTENANCE REPORT — [date]
═══════════════════════════════════════

SITE: [site URL]

PRE-FLIGHT STATUS: ✅ All pages OK

UPDATES APPLIED:
  [✅] plugin-a: 1.0 → 1.1
  [✅] plugin-b: 2.3 → 2.4
  [⚠️] plugin-c: 3.0 → 3.1 — version mismatch, see notes
  [❌] plugin-d: 4.0 → 4.1 — failed, rolled back to 4.0
  [✅] theme-x: 2.0 → 2.1
  [⏭️] WordPress core: 6.7 → 6.8 — skipped per user request

POST-FLIGHT STATUS: ✅ All pages OK
ERROR LOG: 🟡 2 new deprecation notices (non-critical)
MAINTENANCE MODE: ✅ Not active

NOTES:
  - plugin-c shows version 3.1 in files but WordPress
    still reports 3.0. This is a known version metadata
    issue in this release. Monitor for the next update.
  - plugin-d caused a fatal error and was rolled back.
    Consider contacting the plugin developer before
    retrying this update.

SNAPSHOTS RETAINED:
  - All pre-update snapshots preserved for
    future rollback if needed.
═══════════════════════════════════════
```

### Step 7.4: Snapshot Cleanup (Optional)

Ask the user if they want to keep or clean up old snapshots:

- **Keep** (recommended): Snapshots from this session remain available for future rollback
- **Clean**: Delete snapshots from previous maintenance sessions to free disk space

Use `mcm/list-snapshots` to show what's available and `mcm/delete-snapshot` (with user confirmation) to clean up.
