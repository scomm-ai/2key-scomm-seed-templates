# Help them fill; apply on trigger (internal)

**Audience: us.** They never get the billing engine.

Scomm **owns this fork**. They fill and raise PRs. We sit with them on the JSON. We do **not** own their catalog or their PRs.

**Our ops job:** when we get `catalog-seed-updated` for `scomm-ai/2key-scomm-seed-templates`, apply that SHA on the **Scomm billing VM**. Do not apply this fork onto some other tenant’s VM.

```
they fill + PR (we help)
merge to main → dispatch { sha, ref, catalog_repo }
we apply that commit on the Scomm VM
```

Canonical blank: [`2keyapp/2key-seed-templates`](https://github.com/2keyapp/2key-seed-templates).

## This tenant (Scomm)

- GitHub: `scomm-ai/2key-scomm-seed-templates`
- Live files: root `catalog.json` / `auth.json` (not `examples/`)
- Trigger → apply on the Scomm VM only (`BILLING_SEED_DIR` / `--dir` pointing at this checkout @ payload `sha`)

## Next tenant

1. **They** fork `2keyapp/2key-seed-templates` into their org.
2. We help them fill; **they** PR. Shape: template `examples/sample-shop/` — they rename every key.
3. On **their** fork we set `DOWNSTREAM_DISPATCH_TOKEN` and `DOWNSTREAM_REPO`. Canonical template must not dispatch.
4. Ops maps `catalog_repo` → **that** VM.
5. Enable currencies / IdP on **that** VM. On trigger: `billing-seed apply` against **that** DB.

## Sitting with them

Support on **their** branch. If CI is red, they fix (we help). We do not take over the PR.

- [examples/sample-shop/](../examples/sample-shop/) is shape only. Do not copy it over Scomm’s live root.
- `npm ci && npm run validate`; they commit `hosts.json` on their PR.
- Recipes: [recipes.md](recipes.md). Field list: [catalog.md](catalog.md).

## On trigger (apply)

Checkout this repo at `sha`. Against the **Scomm** VM’s DB:

```bash
billing-seed validate --dir .
billing-seed apply --dir .
```

See [ci-and-ops.md](ci-and-ops.md). If apply fails (unknown currency, omitted live SKU), that is a catalog/VM mismatch — we tell them; we do not silently rewrite their JSON.

## Do not

- Apply Scomm’s catalog onto another VM
- Fill and merge as if this repo were ours
- Give them the billing engine, Stripe keys, or SQL
