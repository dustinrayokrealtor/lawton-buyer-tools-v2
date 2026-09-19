# Lawton Buyer Tools

Client-facing buyer tools for Lawton and Southwest Oklahoma, published with GitHub Pages.

Live site: https://dustinrayokrealtor.github.io/lawton-buyer-tools-v2/

| Page | Path |
| --- | --- |
| Landing page | `/` |
| Buyer Payment Toolkit | `/payment-toolkit.html` |
| VA Loan Calculator (household income & residual income) | `/va-loan-calculator.html` |
| Rate Buydown vs Price Cut | `/buydown.html` |
| Buying a Home in Lawton (consult packet) | `/buying-guide.html` |
| What Your BAH Buys at Fort Sill | `/bah/` |
| Moving to Fort Sill | `/fort-sill/` |

Plain static HTML. No build step. Edit a page and push to `main`, and Pages redeploys in a minute or two.

## Lead capture

Every "Print or save as PDF" button runs through `assets/leadgate.js`. The first
click asks for name, email and phone (remembered in that browser), then the page
is snapshotted to a PDF in the browser and posted, with the contact details and a
plain-text summary of the scenario, to a Google Apps Script that emails Dustin,
emails the buyer their copy, and logs the lead to a Google Sheet. The print
dialog opens either way, so a network hiccup never costs a visitor their printout.

One-time setup (about five minutes) is in [`setup/README.md`](setup/README.md).
The web app URL lives in `ENDPOINT` at the top of `assets/leadgate.js`.

Pages that use it: the payment toolkit, the VA loan calculator, the buydown
tool, the BAH calculator, and the buying guide. A page opts in by including the
script and having a `#btn-print` button; an optional `window.LEAD_SUMMARY`
function or `data-lead="Label"` attributes improve the email summary.

## Design language

Every page loads `assets/site.css` first, then its own `<style>` block for
page-specific layout. The shared file holds the design language, matched to
pamandbarry.com so these tools read as part of the same business:

| | Value |
| --- | --- |
| Blue | `#004A9A` — headings, links, figures |
| Red | `#B4090B` — actions and the heading rule only |
| Navy band | `#272D3E` · alt ground `#EAEAEA` · pale `#C2D0E0` |
| Display | Playfair Display, 400, always uppercase |
| Body & UI | Outfit — body, labels, and all figures |
| Geometry | `border-radius: 0` on everything, 2px borders, no shadows or gradients |
| Signature | a 205 × 1.6px rule under every section heading |

Two rules that are easy to break by accident:

- **Nothing is rounded.** One rounded corner and the page stops matching.
- **Red does not go on navy** — it comes out at 1.9:1 and disappears. On dark
  bands the action button and the heading rule both turn white. That inversion
  is already in `site.css`; keep it if you add a dark section.

To restyle everything at once, edit the custom properties at the top of
`assets/site.css`. The old RE/MAX-corporate token names (`--rx-blue`, `--cream`,
`--dark`, and so on) are still defined there, remapped onto the new palette, so
any inline `var(--...)` left in the markup keeps working.

Dustin Ray, Buyer Specialist · Pam & Barry's Team, RE/MAX Professionals · Each Office Independently Owned and Operated.
