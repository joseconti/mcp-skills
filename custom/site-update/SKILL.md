---
name: site-update
description: "Use when performing WordPress site maintenance: updating plugins, themes, or core. Executes a safe update cycle with pre-flight page checks, automatic snapshots, controlled update execution with anti-loop protection, post-update verification, error log inspection, and automatic rollback decisions. Also handles stuck maintenance mode cleanup."
---

# WordPress Site Update & Maintenance

## Working Philosophy

Updates are the most common cause of site breakage. This skill treats every update as a potential risk and applies a **verify → snapshot → update → verify → decide** cycle. Never rush. Never skip verification. Never leave a site in maintenance mode.

If the assistant has browser capabilities, it MUST use them for visual verification of pages before and after updates. If not available, rely on `mcm/site-health` and `mcm/error-log` for verification.

---

## When to Use

- User asks to update plugins, themes, or WordPress core
- A scheduled maintenance task triggers updates
- User asks to check for and apply available updates
- User wants a safe, verified update process with rollback capability

## Inputs Required

- The site URL (to visit pages for visual verification)
- Which updates to apply: all available, or specific plugins/themes/core
- Whether the user wants to approve each update individually or batch them

---

## Execution Order

Follow these phases strictly. Each phase depends on the previous one completing successfully.

| Phase | What to Do |
|-------|------------|
| 0 | Pre-flight: Site health check and page verification |
| 1 | Discovery: List available updates |
| 2 | Planning: Present update plan to user for approval |
| 3 | Snapshot: Backup everything that will be updated |
| 4 | Execution: Apply updates with anti-loop protection |
| 5 | Post-flight: Verify site integrity |
| 6 | Decision: Rollback or confirm |
| 7 | Cleanup: Ensure no maintenance mode remnants |

---

## Reference Files

Detailed instructions for each phase are in the `references/` directory:

- **[pre-flight.md](references/pre-flight.md)** — Phase 0: Site health baseline, page visual checks, error log baseline.
- **[update-execution.md](references/update-execution.md)** — Phases 1–4: Discovery, planning, snapshots, and update execution with anti-loop protection.
- **[post-flight.md](references/post-flight.md)** — Phases 5–7: Post-update verification, rollback decisions, and maintenance mode cleanup.

---

## Critical Rules

### Anti-Loop Protection

Some plugins ship updates with incorrect version metadata. This causes a cycle where the update "succeeds" but `mcm/list-updates` still shows the same plugin as needing an update. **You MUST implement this protection:**

1. **Maximum 2 attempts** per plugin/theme. After the first update, check `mcm/list-updates` for that specific item.
2. If the update still appears after the second attempt, **STOP** and flag it as a potential version mismatch.
3. For flagged items: download the plugin/theme ZIP directly and compare the version header in the main plugin file against what WordPress reports. Report the discrepancy to the user.
4. **Never** attempt a third update for the same item in the same session.

### Maintenance Mode Safety

WordPress creates a `.maintenance` file in the site root during updates. If an update fails mid-process, this file can remain and lock the entire site.

- **After ALL updates complete** (success or failure), always verify that the site is not stuck in maintenance mode.
- Check by visiting the site URL. If it shows "Briefly unavailable for scheduled maintenance", the `.maintenance` file must be removed.
- Use `mcm/delete-maintenance` to check and remove the `.maintenance` file from the WordPress root.
- This check is **mandatory** — it must happen even if all updates succeeded.

### Never Update MCP Content Manager

The plugin `mcp-content-manager-for-wordpress` is the communication bridge. Updating or deactivating it will terminate the session immediately. **Always skip it** in update lists.

---

## Verification Checklist

At the end of a maintenance session, ALL of these must be confirmed:

- [ ] Pre-flight page screenshots/checks were captured
- [ ] All items had snapshots created before updating
- [ ] Each update was verified (max 2 attempts per item)
- [ ] Post-flight page checks match pre-flight (no new errors)
- [ ] Error log was reviewed for new entries
- [ ] Site is NOT in maintenance mode
- [ ] Any failed updates were reported with rollback recommendation
- [ ] User was informed of final status for every item
