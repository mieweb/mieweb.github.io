# mieweb.github.io

The root of `https://mieweb.github.io/`. It holds the files that let `https://mieweb.github.io/...` links open mieweb's mobile apps.

## Why this repo exists

iOS (Universal Links) and Android (App Links) only open an app from an https link if the link's domain says that app may handle it. Phones look for that permission at the **root** of the domain, under `/.well-known/`, and only a repo named exactly `mieweb.github.io` can publish the root. Nothing else lives here.

## How Pulse uses it

A pairing link looks like `https://mieweb.github.io/pulse/open#<pairing details>`. The details are after `#`, so they never reach GitHub.

- **Pulse installed:** the phone opens Pulse straight from the link and Pulse asks to pair. No web page loads.
- **Pulse not installed:** the link opens the `/pulse/open` page, which sends the person to the App Store or Google Play. That page is published from [mieweb/pulse](https://github.com/mieweb/pulse) (`pages/`), not from here.

## Files

| File | What it says |
|---|---|
| `.well-known/apple-app-site-association` | iOS: Pulse (`X5873NL7XM.com.mieweb.pulse`) opens `/pulse/open*` and `/pulse/watch*`. |
| `.well-known/assetlinks.json` | Android: Pulse (`com.mieweb.pulse`) signed with its Play app-signing key or its upload key. |
| `.nojekyll` | Publish as-is, so `.well-known/` is served. |

These are public by design (app IDs and certificate fingerprints). Another mieweb app can add itself by adding an entry to each file.

## Don't

- **Don't set a custom domain** on this repo or any project's Pages. Every `mieweb.github.io` URL would redirect, phones don't follow redirects for these files, and links would quietly stop opening the apps.
- **Don't remove `.nojekyll`.** Without it `.well-known/` isn't published.
