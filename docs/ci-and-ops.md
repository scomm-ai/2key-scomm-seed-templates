# Platform ops (internal)

**Audience: us.** They fork/fill/PR ([README](../README.md), [recipes](recipes.md)). VM mapping: [stand-up.md](stand-up.md).

**Our job:** on `catalog-seed-updated` for **this** `catalog_repo`, apply that SHA on the **Scomm VM**. We do not own their catalog git.

Canonical `2keyapp/2key-seed-templates` does not dispatch.

## What their CI does

1. **Every PR and push** — `npm ci && npm run validate`.
2. **Push to `main`** — `repository_dispatch` `catalog-seed-updated` (`sha`, `ref`, `catalog_repo`).

Apply that payload **only** on the Scomm VM.

## Secrets (we set on this fork)

| Name | Type |
|------|------|
| `DOWNSTREAM_DISPATCH_TOKEN` | Repository secret |
| `DOWNSTREAM_REPO` | Actions variable (`owner/name` of our ops repo) |

Until the handler is live, apply that SHA by hand on the **Scomm** VM — still their JSON.

## Apply

```bash
# this checkout @ the dispatched sha, Scomm billing .env
npm run billing-seed -- validate
npm run billing-seed -- apply
```

## Troubleshooting

| Symptom | Likely cause |
|---------|----------------|
| Apply unknown offering | `offeringCodes` is not a key on `Scomm` offerings. Help them on **their** PR. |
| Apply unknown currency | USD not enabled on **this** VM. |
| Apply refuses to drop a SKU | They deleted a live key. `"isActive": false`. |
| Shop empty / wrong SKUs | Not applied yet, or applied to the wrong VM. |

Schema updates: from billing `npm run catalog-seed:schema`; they pull into **this** fork (we help). Do not hand-edit `schemas/`.
