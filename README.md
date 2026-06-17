# robolist-auth — static pages for eBay OAuth

These two static pages support RoboList's eBay "Connect" flow. They are the source of truth; deploy
them to the public **`adkinsry/robolist-auth`** repository with GitHub Pages enabled (Settings →
Pages → deploy from `main` / root).

| File | Purpose | Deployed URL |
|------|---------|--------------|
| `ebay-callback.html` | Receives eBay's OAuth redirect (`?code=…`) and forwards it to `robolist://ebay/callback` so the app can finish sign-in. | `https://adkinsry.github.io/robolist-auth/ebay-callback.html` |
| `privacy.html` | Privacy policy (eBay requires an https privacy URL that isn't eBay's own). | `https://adkinsry.github.io/robolist-auth/privacy.html` |

## Why this exists
eBay's OAuth only allows **https** redirect/accepted URLs — it rejects custom schemes like
`robolist://…`. The bounce page is a static, secret-free hop: eBay → this https page → the app's
`robolist://ebay/callback` deep link. Consent still happens in the system browser (so Google/Apple/
Facebook sign-in keeps working), and the eBay token exchange happens on-device with the user's own
client secret — no backend.

## eBay Developer portal configuration
On your keyset's RuName / "Your eBay Sign-in Settings" page, set:
- **Privacy Policy URL** → `https://adkinsry.github.io/robolist-auth/privacy.html`
- **Auth Accepted URL** → `https://adkinsry.github.io/robolist-auth/ebay-callback.html`
- **Auth Declined URL** → `https://adkinsry.github.io/robolist-auth/ebay-callback.html`
