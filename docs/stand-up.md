# Help them fill; apply on trigger (internal)

**Audience: us.** They never get the billing engine.

Scomm **owns this fork**. They fill and raise PRs. We sit with them on the JSON. We do **not** own their catalog or their PRs.

**Our ops job:** when we get `catalog-seed-updated` for `scomm-ai/2key-scomm-seed-templates`, apply that SHA on the **Scomm billing VM**. Do not apply this fork onto some other tenant’s VM.

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

## Do not

- Apply Scomm’s catalog onto another VM
- Fill and merge as if this repo were ours
- Give them the billing engine
