# Privy wallet connection

Public App ID: `cmuch5jb100cy0clbkoibiyra` in `public/config.js`.
Never put a Privy App Secret or Glider API key in client files.

`src/privy-wallet.jsx` uses the official Privy React SDK for external Ethereum
wallets on Base. It does not create embedded wallets or transfer money during
connection. Glider still manages portfolio creation, deposits and withdrawals.

Build: `npm ci` then `npm run build`. Test: `npm test` (Node 22+).
The build creates `deployment/index.html` and `deployment/privy-wallet.js` for
the existing static Vercel site; retain its `api/glider.js` backend and server-side
`GLIDER_API_KEY`. The source `public/` site receives the same wallet bundle for
local testing with `server-glider-v2.js`.

In Privy, enable the wallet login method and configure the production origins:

- https://www.basestock10.xyz
- https://basestock10.xyz
- https://base-stock10.vercel.app

For local tests, use a development Privy app or temporarily add the exact
localhost origin. Do not allow wildcard Vercel domains. Check Privy's production
activation before public launch; a development app has a user limit.

Verify the modal opens, wallet cancellation leaves the site usable, account
switching clears prior balances, and disconnect disables withdrawals. Mainnet
signatures/transfers must be tested by the wallet owner, never by automation.
