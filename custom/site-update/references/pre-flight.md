# Phase 0: Pre-Flight Verification

The goal of this phase is to establish a **baseline** of how the site looks and behaves BEFORE any changes. This baseline is what you compare against after updates to detect regressions.

---

## Step 0.1: Site Health Baseline

Run `mcm/site-health` and record:

- WordPress version
- PHP version
- Last fatal error (if any — note the timestamp)
- Paused plugins (if any)
- Memory usage
- Disk space

Save this data mentally as the "pre-update baseline". You will compare against it in post-flight.

---

## Step 0.2: Error Log Baseline

Run `mcm/error-log` with `lines: 20` and note:

- The **last timestamp** in the log. After updates, any entries AFTER this timestamp are new and potentially caused by the updates.
- Any existing fatal errors or warnings. These are pre-existing and should not be confused with update-caused issues.

---

## Step 0.3: Page Visual Verification

This is the most important pre-flight step. You need to verify that key pages load correctly.

### Page Selection Strategy

**If the user has configured specific URLs** (in a config or previous instruction), use those.

**If no URLs are configured**, auto-detect 2-3 representative pages:

1. **Homepage**: The site's main URL (always check this)
2. **A recent post/page**: Use `mcm/search-content` with `post_type: post, per_page: 1, orderby: date` to find the most recent published post
3. **A key functional page** (choose one based on what's installed):
   - If WooCommerce is active → visit the shop page
   - If there's a contact form plugin → visit the contact page
   - Otherwise → visit any page that uses dynamic functionality

### How to Verify Pages

**If browser capabilities are available (preferred):**

1. Navigate to each page URL
2. Take a screenshot and store the reference
3. Check for:
   - Page loads completely (no white screen)
   - No PHP errors visible on the page
   - Layout appears correct (no broken CSS)
   - Key elements are present (header, footer, main content)
   - No "Fatal error" or "Critical error" messages

**If browser capabilities are NOT available:**

1. Use `mcm/site-health` to confirm the site is responding
2. Note the site health status as baseline
3. After updates, you will rely on `mcm/error-log` for regression detection

### Record the Baseline

For each page checked, record:
- URL visited
- Status: OK / Warning / Error
- Any notes (e.g., "existing deprecation notice in footer")

This baseline is compared against in Phase 5 (post-flight).

---

## Step 0.4: Pre-Flight Decision Gate

Before proceeding to updates, verify:

- [ ] Site health baseline recorded
- [ ] Error log baseline timestamp noted
- [ ] At least 2 pages verified as functional
- [ ] No active fatal errors that would make updates risky

**If the site already has fatal errors or paused plugins:**
- Inform the user before proceeding
- Ask if they want to fix existing issues first or proceed with updates anyway
- If proceeding, document the pre-existing issues clearly so they are not confused with update-caused problems

Only proceed to Phase 1 when pre-flight is complete.
