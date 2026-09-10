# Launch funnel review — 2026-09-09

Owner: cmo-pizza-fleet-codex. Review target: `feat/launch-funnel` at `4f7bf87`; base site main: `63643cd`. This document proposes changes; it does not clear the site for paid launch.

## Direction

Lead with the free Clean download. Offer Worlds for $10 once when its delivery path is verified. **Correction after the initial review:** Crew is sold now at $10/month as prepaid early access, with billing starting today and multiplayer not built yet. The previous no-checkout direction below records the earlier review and is superseded. The current source is Pizza Fleet's `docs/marketing/lines.md`, Crew supersession commit `de7098d`; the Worlds funnel merge gate is `417165d`.

Preserve the current visual direction. The immediate work is the route from the hero to the right download, plus truthful availability next to each claim.

## Findings from the current branch

| Finding | Evidence | Next action / owner |
|---|---|---|
| Free download cannot yet deliver an app | The Free card links to `https://github.com/beveryday/pizza-fleet-releases/releases/latest`. `gh release list --repo beveryday/pizza-fleet-releases --json tagName,name,isDraft,isPrerelease,publishedAt --limit 5` returned `[]` during this review. | CTO/release owner publishes and verifies an approved artifact before CMO presents this as an available download. No release was created in this review. |
| Pricing navigation goes to the disclaimer | The header anchor labelled `Pricing` has `href="#cta"`; the price cards have `id="pricing"`. | Site owner changes the target to `#pricing`. |
| Hero still ends in a scroll | Its only action is `Look around`, linking to `#how`. | Once Free delivery works, add `Download free` as the primary action; keep exploration secondary. |
| Crew availability should be visible before reading the price | At the reviewed revision the heading is `$10 a month — the crew`; availability is in the following paragraph. | Superseding direction: plainly state **Crew play is not built yet** before the price and explain billing starts today. Use the current canonical Crew strings; a purchase control is now authorized. |
| Paid copy promises delivery before delivery is verified | Worlds says `Checkout hands you the download on the spot`. Its Payment Link remains a comment slot. | Preserve as staged copy only; do not publish as an available purchase until the actual approved journey works. |
| Above-the-fold collaboration remains ambiguous | Hero says `bring your crew in alongside them`; a later section says realms are single-player today. | Claude CMO truth pass narrows the hero or states the future tense beside that promise. |
| Other capability claims still need build evidence | `Every agent` has `a room of its own`; another section promises tickets, alerts, deploys and revenue connections. | Claude CMO verifies each against the stranger's released build or narrows the exact sentence. This review does not establish these capabilities absent. |

## Fulfillment correction

My earlier direction assumed an in-app Worlds unlock. [CTO PR #7](https://github.com/beveryday/pizza-fleet/pull/7), read directly as a diff in this review, instead describes separate artifacts: a public Clean-only dmg and a paid universal dmg. Adopt that design for the funnel; do not create a runtime unlock requirement on marketing's authority.

The paid function in that diff verifies `payment_status === "paid"`, then redirects to a signed storage URL with `EXPIRES_SECONDS = 600`. This is source evidence, not evidence of a deployed working checkout. [CPO review PR #10](https://github.com/beveryday/pizza-fleet/pull/10) flags that a paid session is not necessarily a Worlds purchase. Route that implementation finding to CTO; do not duplicate its fix here.

Proposed delivery wording after verification: `After checkout, download the Worlds app. Save the installer; its download link expires after ten minutes.` Recovery wording must wait for a demonstrated route back to a fresh download. Do not imply that a conventional receipt email contains that route without evidence, and do not send email to test it.

## Certificate observation

GitHub Pages API for `beveryday/pizza-fleet-site` returned `cname: www.pizzafleet.app`, `https_enforced: false`, and an approved certificate whose domains array contains only `www.pizzafleet.app`. This corroborates the reported configuration mismatch; it is not a fresh apex TLS handshake test. No Pages settings changed. Coordinate the exact settings action and existing approval with Claude CMO/Fable before changing it.

## Ownership and completion

The request to take exclusive ownership of `index.html` and proposed `download.html` remains unanswered in this conversation. This new review document is owned by Codex; existing site files remain untouched. Partner review should settle file handoff and claim corrections before implementation.

Done means: the Free action reaches an approved downloadable Clean package; Worlds reaches the correct one-time purchase and paid package; failure and return paths are explained; Crew clearly discloses that billing starts now for unbuilt multiplayer; platform and prerequisite claims match the packages. Payment/service verification requires an authorized owner under the current GitHub-only constraint. This desk will not call Stripe or Supabase, spend money, send email, or post on social services.

Validation here was read-only GitHub metadata, branch HTML, and PR source inspection. No browser rendering, released-app first-run test, purchase, deployment, or live-site truth clearance was performed.

## Subsequent live-payment sync — received 2026-09-09

The CxO sync message reports these live links; this desk did not open or independently verify them:

- Crew subscription: `https://buy.stripe.com/7sYdR9bZU18WeIX8wF5AQ00`. Preserve it; Brandon's decision to sell prepaid early access supersedes the earlier prohibition. No deactivation is authorized or proposed.
- Worlds Pack: `https://buy.stripe.com/bJecN5aVQaJw30f7sB5AQ01`. The reported redirect has no `STRIPE_SECRET_KEY` or `PAID_DMG_PATH` configured and no fresh universal dmg uploaded, so taking payment does not establish delivery.

Read fresh in the shared product repo: `lines.md` at `417165d` expressly gates the funnel-branch merge on **one verified end-to-end purchase that actually delivers a download**. That gate binds this desk too. A test purchase is Brandon's action to arrange; this desk will not charge money to satisfy it. The old no-Crew-button gate is superseded, not the Worlds delivery gate.

The same sync reports an unauthenticated phase/reset defect in `lib/realm-relay.js` and an unresolved Supabase Auth signup/email/domain-allowlist check. Route the former to CTO as relevant to live revenue and the latter to Brandon's dashboard action. Both remain unverified by this desk; neither supports a claim that multiplayer or account signup works today. Claude CMO retains the canonical ledger and checkout-copy ownership.
