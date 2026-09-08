# Alworth & Reed — Open Items

Last updated: August 2026
Site is live at www.alworthreednotary.com. Phases A–G complete.

---

## Phase I — Online booking

**Decision made:** Cal.com, two free individual accounts (one per notary).
Square Appointments was ruled out — its free tier is single-user, and multi-staff
starts at $29/mo. Calendly's free tier allows only one event type and one calendar
connection. Google's own appointment scheduling requires paid Workspace, so it
won't run on free Gmail.

Cal.com free includes unlimited event types, unlimited calendar connections
(both women have several), email/SMS notifications, and Stripe payments.

**Round-robin is deliberately deferred.** Two separate booking links, one per
notary, cost nothing. A single shared link that alternates between them requires
Cal.com Teams at $15/user/month. Revisit only if the two-link approach annoys them.

### Steps

1. Katie and Chrissy each sign up at cal.com with their existing Gmail
   - Usernames: `katie-alworth`, `chrissy-reed`
   - Connect Google Calendar during signup — this is what prevents double-booking
   - Set available hours
2. Build event types from the rate card: General Notarization, Loan Signing,
   After-Hours. Set durations, travel buffers, deposit amounts.
3. Consider a Stripe deposit at booking. A no-show costs an hour of driving.
4. Site swap — see BOOKING SWAP POINT comment in `index.html`:
   - Point the gold hero button and the "Book by Phone" button at the scheduler
   - Replace the dashed QR placeholder with a generated QR image

---

## Email — current state (supersedes earlier notes)

Cloudflare Email Routing has been **disabled**. The domain now runs on a paid
Google Workspace tenant, billed since Aug 9.

- MX: single record, `smtp.google.com`, priority 1
- Working mailboxes: `creed@` (Chrissy), `kalworth@` (Katie) — both send and receive
- Site contact block links these two directly, labeled by person

**`info@alworthreednotary.com` does not exist and bounces.** It is printed on the
rate card and banner. Removed from the website. Fix by creating it as an alias
once admin access is restored — no reprinting needed.

**Blocker: no one can sign into admin.google.com.** Google's own email names
`creed@alworthreednotary.com` as the admin, but that account loops at the sign-in
picker, including in a clean private window, and shows no Admin app icon.
Tried and ruled out: multiple signed-in Google accounts, private browsing.

This blocks: creating `info@`, adding users, DKIM setup, billing changes.
Recovery path — Google Workspace support, included in the subscription. They
verify via domain ownership, which is straightforward since we control DNS.
Have ready: domain, Aug 9 billing confirmation, billing email (coggireed@gmail.com).

Also still outstanding: **DKIM is not configured.** Admin console → Apps →
Google Workspace → Gmail → Authenticate email. Improves deliverability.
Blocked on admin access.

---

## Parked, in priority order

### 1. Google Business Profile
Bigger lead driver than the website for a local notary. The site makes the
profile credible; the profile is what gets found. Highest-value remaining item.

### 2. Test both phone numbers from a real phone
925-550-0158 and 415-806-4517. Verified on desktop only so far.
Confirm both launch the dialer on iOS and Android.

### 3. Chrissy's headshot
Current image is 1024px and visibly softer than Katie's studio shot. It's held
inside a 112px circle, which hides it. Do not enlarge that container without a
higher-resolution source. Recommend a matching studio session for both.

### 4. "Licensed" → "Commissioned"
California notaries are commissioned, not licensed. The website already uses the
correct term. The printed rate card and banner still say LICENSED — fix on the
next print run.

### 5. DBA filing, Contra Costa County
Notary commissions are individual, not corporate. Operating under the trade name
"Alworth & Reed" generally wants a fictitious business name statement.

### 6. Instagram — resolved
The Instagram account is **@eastbaymobilenotary**, not @alworthreednotary.
This is confirmed correct — the handle intentionally differs from the business
name. Linked in the site contact block. Do not "fix" this.

Note: the `?stkn=` parameter Instagram appends when copying a link from the app
was stripped. It's a session-tied share token and doesn't belong in a permanent link.

### 7. Verify the notarial fee cap annually
$15 per signature, set by California Government Code §8211. Verified current as of
August 2026. Re-check yearly — it has changed before, and publishing a fee above
the statutory cap is a real compliance problem.

---

## Reference

| Item | Value |
|---|---|
| Live site | www.alworthreednotary.com |
| Repo | github.com/tjrebay/alworth-reed |
| Host | Cloudflare Pages, project `alworth-reed` |
| Preview URL | alworth-reed.pages.dev |
| DNS | Cloudflare (registrar remains GoDaddy) |
| Email | Cloudflare Email Routing → Gmail (inbound only) |
| Redirect | Apex → www, 301, query string preserved |

**Known limitation:** Email Routing is inbound only. Replies go out from the
personal Gmail address, not `info@alworthreednotary.com`. Fine for most inquiries;
may look off to escrow officers. Revisit only if it becomes a real problem.

**Deploy:** any push to `main` redeploys automatically. No build step.
Do not commit `preview.html` — it's a 1.5 MB base64 duplicate for emailing only.
