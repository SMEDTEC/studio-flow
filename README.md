# Connected Compliance — SMEDTEC Studio

An interactive walkthrough of how SMEDTEC Studio wires a brand's existing tools — suppliers, labs, commerce, chat, project boards, registers — into one compliance layer the client owns. It shows the system reasoning over evidence and proposing actions, while every decision stays with the user.

**Live demo:** (https://smedtec.github.io/studio-flow/)

> Visualisation only. A real build is wired to a client's actual tools and suppliers; nothing here is templated.

---

## What it shows

A single screen with three things working together:

- **A live connection map.** The compliance layer sits in the centre; inputs (suppliers, test labs, commerce/PIM, live rule changes) feed in from the left; outputs (chat, project tool, registers, email) sit on the right. The left-to-right layout reads as the argument: inputs become compliance state, which becomes actions.
- **Six flows you can run.** A supplier test report arriving, adding a product claim, a market changing its rules, a product entering a new market, a customer reaction, and a retailer requesting a compliance pack. Each animates a real event moving across the connected tools.
- **AI that reasons, never decides.** When a flow reaches a judgement, the AI shows its reasoning and a recommendation, then hands the decision to the user with Approve / Send-for-review. The action it produces is mapped to a specific product and SKU, and stays "Awaiting your approval" until the user acts.

It also stays alive at rest: live counters in the hub, an ambient regulatory activity feed, a "last sync" clock, pulsing connection points and drifting data, plus a short guided tour on first visit.

---

## Using it in a call or an email

- **Walk a prospect through it** with the built-in tour, or press play on the flow closest to their world (the customer-reaction flow is the clearest demonstration of "AI reasons, you decide").
- **Send a pre-branded link.** Set the company name and switch off the tools they don't use, then copy the link. It opens already configured for them.

### Shareable link parameters

State is held in the URL after `#`, so any configuration is shareable and bookmarkable:

- `c=` — company name (URL-encoded), e.g. `c=Synergie%20Skin`
- `off=` — tools switched off, by id, joined with `-`
- `s=` — the flow shown first

Tool ids: `sup` (suppliers), `lab` (test labs), `pim` (commerce/PIM), `reg` (rule changes), `slack`, `tasks` (project tool), `data` (registers), `email`.
Flow ids: `report`, `claim`, `rule`, `market`, `adverse`, `retailer`.

Example — built for an Australian brand that doesn't use the regulatory feed or email, opening on the customer-reaction flow:

```
https://smedtec.github.io/connected-compliance/#c=Synergie%20Skin&off=reg-email&s=adverse
```

A returning visitor's setup is also remembered in their browser.

---

## Make it your own

Everything lives in one file (`index.html`). Open the `<script>` block and edit these, near the top:

- **`NODES`** — the connected tools. Change the names and the plain-English roles to match a prospect's actual stack (for example, swap "Slack" for "Microsoft Teams", or "Commerce / PIM" for their PIM).
- **`SCENARIOS`** — the flows. Each step can carry narration, an `ai` reasoning block, or an `action` card. The sample products, SKUs and claims sit inside the `action` objects — change them to a prospect's real range.
- **`FEED_LINES`** — the ambient activity feed. These are written in regulatory language (CPSR, MoCRA, UK SCPN, EU CPNP, UKCA, ISO 13485, ISO 24444, vigilance). Edit to suit the brand's markets.
- **`:root`** in the stylesheet — brand tokens. Navy `#2E3F57`, teal `#00C5A8`, gold `#D98A1F` (reserved for the statutory tile only). British spelling throughout, no emoji.

No build step and no dependencies, so an edit is just a save. To sanity-check a change before deploying, you can extract the script and run `node --check` on it.

---

## Deploying (GitHub Pages)

GitHub Pages serves the file named `index.html` at the repository root.

1. Name the deploy file exactly `index.html` (Pages will not serve `compliance-flow-demo.html` or `index v2.html`).
2. **Add file → Upload files**, drag in `index.html`, and commit.
3. In **Settings → Pages**, set the source to the `main` branch, root folder, and turn on **Enforce HTTPS**.
4. Hard-refresh after each update (`Ctrl/Cmd + Shift + R`) to clear the CDN cache.

To keep it in the existing `studio-demo` repo instead of its own, drop the file at `flow/index.html` and it serves at `https://smedtec.github.io/studio-demo/flow/`.

### Optional: a custom domain

A clean address reads better in a prospect's inbox than the `github.io` path. To use, say, `flow.smedtec.co.uk`:

1. Add a DNS **CNAME** record at your domain host: `flow` → `smedtec.github.io`.
2. Once that record exists, set the custom domain in **Settings → Pages** (this creates a `CNAME` file in the repo).
3. Leave **Enforce HTTPS** on.

Add the custom domain only after the DNS record is live, or the default address can stop resolving.

---

## Repo About panel

Paste into the repository's About panel:

- **Description:** Interactive demonstration of how SMEDTEC Studio connects a brand's tools, suppliers and evidence into one owned compliance layer.
- **Website:** https://smedtec.github.io/connected-compliance/
- **Topics:** `smedtec`, `compliance`, `regulatory-affairs`, `consumer-health`, `cosmetics`, `medical-devices`, `integration`, `product-management`, `demo`

---

## How it's built

A single self-contained HTML file: HTML, CSS and vanilla JavaScript, no framework and no build pipeline. Typography (DM Sans, JetBrains Mono) loads from Google Fonts. SVG draws the connection lines; the rest is plain DOM. It is responsive, keyboard-focusable, and respects `prefers-reduced-motion` — the drifting data, ripples and breathing switch off, leaving the settled state intact.

Because it is static, it runs anywhere that serves files. Browser storage (the tour-seen flag and a remembered setup) works on a live host; it is harmless if blocked.

---

## A note on the AI

The AI in this demo reasons over the evidence and drafts the action. It does not decide. Approving, holding, or overriding an action is always the user's, and whether something is reportable to a regulator is treated as the regulated judgement it is. That principle is stated on screen and is the point the demo is built around.

---

## Related

- SMEDTEC Studio (the product demo): https://smedtec.github.io/studio-demo/

---

Proprietary to SMEDTEC Ltd. See `LICENSE`.
SMEDTEC Ltd · Manchester, United Kingdom · info@smedtec.co.uk
