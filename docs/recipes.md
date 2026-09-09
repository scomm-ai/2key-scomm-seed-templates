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
- Add-on label in apps → `displayName` on that **offering** (under `offerings`)

Do not change the quoted **key**.

## Stop selling

On the plan (or offering) set `"isActive": false`. Do **not** delete the key.

## Add an add-on or app

You add the keys. Your billing contact will sit with you. Then `npm ci && npm run validate`, commit `hosts.json` if it changed, open a PR. Field list: [catalog.md](catalog.md).

## First-login emails

Root [`auth.json`](auth.md) is yours to change (no passwords). You open the PR.

A green PR is not in the shop until we apply on the Scomm VM.
