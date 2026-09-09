# `auth.json`

Scomm’s first-login emails are **root** `auth.json`. You change this file (billing contact helps) and **you** open the PR. `examples/auth/` is not the live list.

**Never put passwords or IdP secrets in this file.** Sign-in is the identity provider **we configure** on the Scomm VM.

Keep `"$schema": "./schemas/auth.schema.json"` at the top.

This does **not** grant complimentary subscriptions. Buying stays in the portal after sign-in.

## Shape

See [`examples/auth/auth.json`](../examples/auth/auth.json). That file is not a real customer.

| You fill | Key | Meaning |
|----------|-----|---------|
| `users` | Email | Person who can sign in. |
| `organizations` | Org slug | Stable handle (not the display name). |
| `members` | Email | Must already appear under `users`. |
| `payingParty` | — | At most one per org. Billing email for that org. |
