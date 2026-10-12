# mieweb.github.io

The root of `https://mieweb.github.io/`. It exists to serve the app-association files that let `https://mieweb.github.io/...` links open mieweb's mobile apps (iOS Universal Links, Android App Links). Phones only look for these files at the domain root, and only a repo with this exact name can publish the root.

Each project's own pages stay in that project's repo: `https://mieweb.github.io/pulse/` is published from [mieweb/pulse](https://github.com/mieweb/pulse) (`pages/`).

## Files

| Path | What |
|---|---|
| `.nojekyll` | Publish as-is, so `.well-known/` is served. |
| `.well-known/apple-app-site-association` | iOS: `X5873NL7XM.com.mieweb.pulse` handles `/pulse/open*` (pairing links) and `/pulse/watch*` (watch links). |
| `.well-known/assetlinks.json` | Android: `com.mieweb.pulse`, signed with its Google Play app-signing key (store installs) or its upload key (CI builds installed directly). |

These files are public by design: they hold app IDs and certificate fingerprints, nothing secret. Another mieweb app can add itself by appending an entry to each file.

## Rules

- **Never set a custom domain** on this repo or on any project's Pages. It turns every `mieweb.github.io` URL into a redirect, phones do not follow redirects for these files, and the links silently stop opening the apps.
- Pages publishes from `main`, `/` (branch deploy). Keep `.nojekyll`.
- Debug-signed Android builds are not listed, on purpose: the React Native template's debug keystore is the same in every project, so listing it would let any app signed with it claim these links. Test those builds against a separate test host.

## Checks

```sh
# Served without a redirect
curl -sI https://mieweb.github.io/.well-known/apple-app-site-association
curl -sI https://mieweb.github.io/.well-known/assetlinks.json

# What Apple's CDN cached (this is what iPhones read; it can lag by hours)
curl -s https://app-site-association.cdn-apple.com/a/v1/mieweb.github.io

# What Google's verifier reads
curl -s "https://digitalassetlinks.googleapis.com/v1/statements:list?source.web.site=https://mieweb.github.io&relation=delegate_permission/common.handle_all_urls"

# On an Android phone with Pulse installed
adb shell pm get-app-links com.mieweb.pulse
```
