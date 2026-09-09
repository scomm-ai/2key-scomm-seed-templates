# Change the shop (Scomm)

This is **your** [`catalog.json`](../catalog.json). Edit it, open a pull request. Your billing contact will help. You do not run apply — we apply when this fork triggers the **Scomm VM**.

Shop card **titles** are the plan keys below. Search the file for the quoted name.

## Your plan keys

| Shop title | Offering key (do not rename) |
|------------|------------------------------|
| Outlook OpenPGP ECC | `pgp` |
| Outlook OpenPGP ECC+PQC | `pqc` |
| Linux Version | `linux` |
| Local-AI | `ai_assistant` |
| SComm Connect | `scomm_connector` |
| Custom Colours & Backgrounds | `accent_color` |
| AI Tokens 1M | `ai_tokens_1m` |

Product key: `"Scomm"`. Apps: `scommDesktop`, `scommLinux`, `office`. Surfaces: `scomm`, `office`.

## Change a price

Find the plan, then edit `basePrice`. Leave the plan name and `"annual"` / `"monthly"` keys alone.

```json
"SComm Connect": {
  "pricings": {
    "annual": { "currency": "USD", "basePrice": 5 }
  }
}
```

Change `5` to the new amount. Keep `"USD"`.

## Change the text customers see

- Plan blurb → `description` on that **plan**
- Add-on label in apps → `displayName` on that **offering** (under `offerings`, not `plans`)

Do not change the quoted **key**.

## Stop selling

On the plan (or offering) set `"isActive": false`. Do **not** delete the key. If anyone still subscribes, apply will fail.

## Add an add-on or app

You add the keys. Your billing contact will sit with you.

1. Put the offering under `products.Scomm.offerings` (give it `resources.surfaces` that match a host).
2. Put a plan under `plans` with `offeringCodes` pointing at that offering key.
3. `npm ci && npm run validate` — commit `hosts.json` if it changed.
4. Open a PR.

Field list: [catalog.md](catalog.md). Do not copy [examples/sample-shop/](../examples/sample-shop/) over the live root.

## First-login emails

Root [`auth.json`](auth.md) is yours to change (no passwords). You open the PR.

## Hard rules

| Do not | Why |
|--------|-----|
| Rename a live key | New SKU, not a rename. Add a new key; hide the old one. |
| Delete a key people still pay for | Apply fails. Use `"isActive": false`. |
| Hand-edit `hosts.json` / `schemas/` | Validate writes hosts; we ship schemas. |

A green PR is not in the shop until we apply on the Scomm VM.
