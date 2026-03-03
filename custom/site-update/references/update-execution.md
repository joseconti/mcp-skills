# Phases 1–4: Discovery, Planning, Snapshots & Update Execution

---

## Phase 1: Discovery — List Available Updates

### Step 1.1: Refresh Update Transients

WordPress caches update information. Before listing updates, refresh the cache:

```
mcm/run-cron-event → hook: "wp_update_plugins"
mcm/run-cron-event → hook: "wp_update_themes"
```

Wait a moment after triggering these cron events before checking for updates.

### Step 1.2: List All Available Updates

Run `mcm/list-updates` with `type: "all"` to get:

- Core updates (WordPress itself)
- Plugin updates
- Theme updates
- Translation updates

### Step 1.3: Filter Out Protected Items

**Always remove from the update list:**

- `mcp-content-manager-for-wordpress` — NEVER update during a session. Doing so terminates the MCP connection immediately.
- Any plugin/theme the user has explicitly asked to skip.

### Step 1.4: Identify Premium/Licensed Items

Use `mcm/verify-plugins` to check which plugins are from WordPress.org vs. premium/custom.

Premium plugins with inactive licenses may appear to have updates but will fail with "You already have the latest version". Flag these to the user before attempting the update.

---

## Phase 2: Planning — Present Update Plan

Present the update list to the user in a clear format:

```
Updates available:

PLUGINS (X items):
  - plugin-name: 1.2.3 → 1.3.0
  - another-plugin: 4.0.1 → 4.1.0
  - [PREMIUM] premium-plugin: 2.0 → 2.1 ⚠️ May require active license

THEMES (X items):
  - theme-name: 3.0 → 3.1

CORE:
  - WordPress: 6.7 → 6.8 (requires confirm=true)

TRANSLATIONS:
  - X translation updates available
```

Ask the user:
1. Do you want to update everything, or select specific items?
2. For core updates: confirm explicitly (these are higher risk)
3. Should translations be updated too?

**Do not proceed until the user approves the plan.**

---

## Phase 3: Snapshot — Create Backups

Before touching anything, create snapshots of every item that will be updated.

### Step 3.1: Create Plugin Snapshots

For each plugin to be updated:

```
mcm/create-snapshot → type: "plugin", slug: "plugin-folder/plugin-file.php"
```

Record the snapshot ID for each plugin. You will need these for potential rollback.

### Step 3.2: Create Theme Snapshots

For each theme to be updated:

```
mcm/create-snapshot → type: "theme", slug: "theme-slug"
```

Record the snapshot ID for each theme.

### Step 3.3: Verify Snapshots

After creating all snapshots, run `mcm/list-snapshots` and confirm that a snapshot exists for every item in the update plan. **Do not proceed if any snapshot is missing.**

---

## Phase 4: Execution — Apply Updates with Anti-Loop Protection

### Update Order

Apply updates in this specific order to minimize risk:

1. **Translations first** (lowest risk)
2. **Plugins** (one at a time, verify each)
3. **Themes** (one at a time, verify each)
4. **Core last** (highest risk, requires `confirm: true`)

### Step 4.1: The Update-Verify Cycle

For each item, follow this exact cycle:

```
┌─────────────────────────────────────────────────┐
│  ATTEMPT 1                                       │
│                                                   │
│  1. Run mcm/run-update for the item               │
│  2. Check result: success or failure?              │
│  3. Run mcm/list-updates for this specific item    │
│  4. Is the item still in the update list?          │
│     ├─ NO  → ✅ Update confirmed. Move to next.   │
│     └─ YES → Go to ATTEMPT 2                      │
│                                                   │
├─────────────────────────────────────────────────┤
│  ATTEMPT 2                                       │
│                                                   │
│  1. Run mcm/run-update again for the same item     │
│  2. Check result: success or failure?              │
│  3. Run mcm/list-updates for this specific item    │
│  4. Is the item still in the update list?          │
│     ├─ NO  → ✅ Update confirmed. Move to next.   │
│     └─ YES → ⚠️ VERSION MISMATCH DETECTED         │
│              Go to Step 4.2                        │
│                                                   │
└─────────────────────────────────────────────────┘
```

### Step 4.2: Version Mismatch Handling

When an item appears to update successfully but still shows in the update list after 2 attempts:

1. **Do NOT attempt a third update.** This is likely a version metadata error in the plugin/theme.

2. **Diagnose the issue:**
   - Use `mcm/read-file` to read the main plugin file header and check the `Version:` line.
   - Compare the version in the file header against what `mcm/list-updates` reports as the "current" and "new" versions.
   - If the file shows the new version but WordPress still lists it as needing an update → **this is a plugin-side version metadata bug**.

3. **Try direct download as fallback:**
   - If the plugin is from WordPress.org, use `mcm/install-plugin` with the slug to force-download a fresh copy.
   - If it's a premium plugin, inform the user that the update may require manual intervention through the plugin's license/dashboard.

4. **Report to user:**
   ```
   ⚠️ Version mismatch detected for [plugin-name]:
   - File header version: X.Y.Z
   - WordPress expected version: A.B.C
   - Update list still shows update available after 2 attempts
   - This is likely a version metadata error in the plugin release.
   - Recommendation: [specific recommendation based on diagnosis]
   ```

### Step 4.3: Handling Update Failures

If `mcm/run-update` returns `success: false`:

1. Check `mcm/site-health` immediately — look for fatal errors or paused plugins.
2. Check `mcm/error-log` for new entries.
3. If the site is broken (fatal error detected):
   - **Immediately rollback** using `mcm/restore-snapshot` with the snapshot ID created in Phase 3.
   - Inform the user of the failure and rollback.
   - **Stop all remaining updates** — do not continue if one update caused a fatal error.
4. If the site is functional but the update just failed:
   - Report the failure to the user.
   - Ask whether to skip this item and continue with the remaining updates.

### Step 4.4: Core Update Specifics

WordPress core updates are the highest risk:

1. Always do core updates **last**, after all plugins and themes are updated.
2. Require explicit `confirm: true` parameter.
3. After core update, immediately run `mcm/site-health` — core updates can break plugin compatibility.
4. If the core update causes issues, you cannot easily rollback core — inform the user of this risk before starting.

### Step 4.5: Update Tracking

Maintain a running log during execution:

```
UPDATE LOG:
──────────
[✅] translations — all updated
[✅] contact-form-7: 5.9.1 → 5.9.2 — verified
[✅] woocommerce: 9.3.0 → 9.4.0 — verified
[⚠️] premium-seo: 4.0 → 4.1 — version mismatch after 2 attempts
[❌] broken-plugin: 1.0 → 1.1 — failed, rolled back
[⏭️] remaining-plugin: skipped (user chose to stop after failure)
```

This log is presented to the user in Phase 6.
