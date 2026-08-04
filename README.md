# Faz Tandoors

Pre-launch landing page. Collects the waitlist for opening night, January 2027.

Live at: *(add your Netlify URL here)*

---

## The only file that matters

`index.html` — everything is in it. No build step, no dependencies, no
framework. Open it in a browser and it works. Netlify serves it as-is.

## Configuration

Near the bottom of `index.html`, in the `<script>` block:

```js
var CONFIG = {
  BUTTONDOWN_USERNAME: "faztandoors",
  LAUNCH: "2027-01-07T17:00:00-07:00",
  FOUNDING_PLACES: 50,
  CLAIMED: 0,
  DEFAULT_TAG: "website"
};
```

| Key | What it does |
|---|---|
| `BUTTONDOWN_USERNAME` | Public username the signup forms post to. Not a secret. |
| `LAUNCH` | Target for the hero countdown. First Thursday of 2027. |
| `FOUNDING_PLACES` | Denominator on the ember gauge. |
| `CLAIMED` | **Update this as reservations land.** Drives how many coals glow. |
| `DEFAULT_TAG` | Tag applied to signups with no `?tag=` in the URL. |

Leaving `BUTTONDOWN_USERNAME` empty puts the page in test mode: forms work
end to end, nothing leaves the browser. Useful for checking copy changes.

---

## Never put an API token in this file

Everything in `index.html` is public — anyone can read it with View Source,
and bots scan live sites for exposed keys continuously.

Signups use Buttondown's **embed endpoint**, which is designed for exactly
this and requires no credentials:

```
https://buttondown.com/api/emails/embed-subscribe/faztandoors
```

Buttondown's admin API (`api.buttondown.email`) needs a token, blocks
browser-origin requests via CORS, and would grant whoever found the token
the ability to export the entire subscriber list. It is the wrong tool here.
If something ever genuinely needs a secret, it belongs in a Netlify
environment variable behind a serverless function, never in this file.

---

## Tracking where signups come from

The form reads `?tag=` off the URL and passes it to Buttondown, so each
channel can be measured separately:

| Where | URL to print or send |
|---|---|
| Plain site | `faztandoors.com` |
| Cookout QR code | `faztandoors.com/?tag=cookout-aug-15` |
| Business card | `faztandoors.com/?tag=card` |
| Nextdoor post | `faztandoors.com/?tag=nextdoor` |

Use a fresh tag per event. After a few cookouts the tag breakdown in
Buttondown tells you which crowd is actually worth the Saturday.

Every signup also gets `form-hero` or `form-footer` so you can see which
half of the page converts.

**Buttondown uses double opt-in.** A submitted address is not a subscriber
until they click the confirmation link. Expect roughly 60% to confirm, and
say so out loud at cookouts — it noticeably raises the rate.

---

## Deploying

Once the repo is linked to Netlify:

- Build command: *(leave empty)*
- Publish directory: `/`
- Branch: `main`

Every push to `main` redeploys. Deploy history gives you one-click rollback.

## Editing without a terminal

GitHub's web editor is enough for everything here: open `index.html`, click
the pencil, change the copy, commit to `main`. Netlify rebuilds in seconds.
Bumping `CLAIMED` as founding places sell is a ten-second edit.

---

## Before the January launch

- [ ] Confirm the CDPHE cottage food registration process with Boulder County Public Health (303-441-1564)
- [ ] Complete the TCS food safety course
- [ ] Verify the label disclaimer wording against CDPHE's post-2027 rules
- [ ] Check the Shan masala box for sub-ingredients that need declaring
- [ ] Test a version without red food coloring
- [ ] Turn on real payment before accepting founding-50 money
