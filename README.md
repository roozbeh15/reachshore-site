# reachshore.com — static landing page

Single-file static landing page for ReachShore. Deployable in 20 minutes.

## What's here

- `index.html` — the entire site. Inline CSS and JS, no build step, no dependencies.
- One Inter font import from Google Fonts (the only external request)
- Inline SVG favicon (replace later)

## Three URLs you must replace before going live

Search and replace these in `index.html`:

| Token | What to put | Example |
|---|---|---|
| `REPLACE_WITH_STRIPE_PAYMENT_LINK` | Your Stripe Payment Link for the $99 deposit | `https://buy.stripe.com/abc123` |
| `REPLACE_WITH_CALENDLY_LINK` | Your Cal.com or Calendly URL for 15-min discovery calls | `https://cal.com/roozbeh/15min` |
| `REPLACE_WITH_WAITLIST_ENDPOINT` | Form endpoint for waitlist email capture (Formspree / ConvertKit / Resend) | `https://formspree.io/f/abc123` |

Until you replace them, the deposit and Calendly buttons go nowhere and the waitlist form just logs to console (with a friendly fake-success message).

## Deploy in 20 minutes — Vercel (easiest)

1. Go to [vercel.com/new](https://vercel.com/new)
2. Drag the `reachshore-site` folder onto the page
3. Click Deploy
4. You'll get a `*.vercel.app` URL within 30 seconds
5. In the project's Domains settings, add `reachshore.com` and `www.reachshore.com`
6. Update DNS at your registrar (Porkbun / Namecheap):
   - For apex: `A` record → `76.76.21.21` (Vercel's IP)
   - For www: `CNAME` → `cname.vercel-dns.com`
7. Wait 10–60 minutes for DNS to propagate
8. Done. SSL is automatic.

## Alternative: Cloudflare Pages

1. Push this folder to a new GitHub repo
2. Go to [pages.cloudflare.com](https://pages.cloudflare.com) → Create project
3. Connect to GitHub, pick the repo, click Deploy
4. Add custom domain `reachshore.com` in Pages settings
5. Cloudflare auto-handles DNS if your domain is on Cloudflare; otherwise add the CNAME they give you

## Alternative: Netlify Drop (drag-and-drop)

1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag the `reachshore-site` folder
3. Add domain in site settings

## Form / payment wiring (do today)

### Stripe Payment Link

1. Stripe Dashboard → Payment Links → New
2. Product: "ReachShore — Founder Pricing Deposit"
3. Price: $99 USD, one-time
4. **Important:** Set capture mode to **Manual** (lets you cancel/refund without dispute)
5. Optional: enable receipt emails
6. Save the URL, paste it into `index.html` replacing `REPLACE_WITH_STRIPE_PAYMENT_LINK`

### Cal.com / Calendly

1. Create a 15-min event type
2. Title: "ReachShore — 15-min discovery"
3. Availability: weekdays 9am–5pm in your timezone
4. Add buffer: 5 min before, 10 min after
5. Send the URL, paste into `index.html` replacing `REPLACE_WITH_CALENDLY_LINK`

### Waitlist endpoint

Pick one:

**Formspree (easiest, free for 50/mo):**
1. Sign up at [formspree.io](https://formspree.io)
2. Create a new form, get the action URL like `https://formspree.io/f/xyzabc`
3. Replace `REPLACE_WITH_WAITLIST_ENDPOINT` in `index.html`

**Resend (best for control, free tier 3k/mo):**
1. Build a tiny serverless function (Vercel / Cloudflare Worker) that POSTs `{ email }` to your DB or Resend audience
2. Replace `REPLACE_WITH_WAITLIST_ENDPOINT` with that URL

**ConvertKit (if you want email marketing later):**
1. Get your form endpoint from ConvertKit
2. Adjust the JS in `index.html` to match ConvertKit's expected payload

## Customizations to consider after launch

- Replace the inline SVG favicon with a real logo (`favicon.ico`, `favicon.svg`)
- Add OG image at `og-image.png` (1200×630), update `<meta property="og:image">`
- Embed a live X feed in the "build in public" section once you have posts
- Add Plausible (`<script defer data-domain="reachshore.com" src="https://plausible.io/js/script.js"></script>`) or GA4 for analytics
- Add a Cookie banner if/when you take EU traffic (Plausible doesn't need one)
- Update the Tend pilot stats card with real numbers as Phase B runs

## Performance & SEO baseline

- Lighthouse scores at first deploy should be 95+ across the board
- Page is ~30kb HTML, ~1 external font request
- No analytics, no trackers, no JS frameworks — all by design
- Fully accessible: skip link, semantic landmarks, proper heading order, sufficient contrast

## When you've gone live

Send me the URL and I'll review it for:
- Copy clarity
- CTA hierarchy
- Conversion friction
- Anything obviously broken

That's a 10-min review and worth doing before driving the first traffic.
