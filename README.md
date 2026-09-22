# alworthreednotary.com

One-page static site for Alworth & Reed Concierge Notary.
No build step. No dependencies. Edit `index.html` and push.

## Structure

```
index.html          entire site — markup and CSS in one file
assets/logo.png     A|R seal, transparent background
assets/katie.jpg    Elizabeth "Katie" Alworth, 760x760
assets/chrissy.jpg  Chrissy Reed, 760x760
```

## Local preview

Open `index.html` in a browser, or:

```
python3 -m http.server 8000
```

## Cloudflare Pages settings

| Field | Value |
|---|---|
| Framework preset | None |
| Build command | *(leave empty)* |
| Build output directory | `/` |

## Deploy sequence

1. Push to GitHub `main`
2. Cloudflare → Workers & Pages → Create → Pages → Connect to Git
3. Verify on the `*.pages.dev` URL
4. Cloudflare → Add a site → `alworthreednotary.com` → Free plan
5. GoDaddy → Manage DNS → Nameservers → replace with Cloudflare's two
6. Wait for zone activation email
7. **Delete the stale `A @ → WebsiteBuilder Site` record**
8. Pages project → Custom domains → add `www.alworthreednotary.com`, then apex
9. Redirect Rule: apex → `www`
10. Cloudflare → Email Routing → forward `info@alworthreednotary.com` to Gmail

## Editing

Phone numbers appear in `tel:` links and as display text. Search `9255500158`
and `4158064517` to find all instances.

Prices are plain text inside `<span class="price">` elements in the pricing
section. Nothing is calculated.

## Notes

- The NSA badge in the credentials section is **hot-linked** to
  nationalnotary.org per the NNA's own badge-embed code. It is not self-hosted,
  so it breaks if the NNA moves the file. Verify it still renders after any
  NNA site redesign.
- Katie's verification link points to her signingagent.com profile, which is
  NNA-hosted and shows whatever she has entered under Manage Profile —
  including her loan-document delivery address. Changes there appear on the
  public site immediately.
- Chrissy has no signingagent.com profile yet. A commented-out second verify
  link sits in the credentials section, ready for her profile ID.
- California notarial fee cap ($15/signature) is set by Gov. Code §8211.
  Re-verify annually.
- Chrissy's headshot is 1024px and displays inside a 230px circle. Do not
  enlarge that container without a higher-resolution source.
