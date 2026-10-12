# .well-known

Read by phones to decide which app may open `https://mieweb.github.io/...` links.

- `apple-app-site-association`: iOS opens Pulse (`X5873NL7XM.com.mieweb.pulse`) for `/pulse/open*` (pairing) and `/pulse/watch*` (watch, later).
- `assetlinks.json`: Android opens Pulse (`com.mieweb.pulse`) when it's signed with the Play app-signing or upload key.
- **Why:** a pairing link opens Pulse straight away when installed; otherwise it opens the `/pulse/open` page (from [mieweb/pulse](https://github.com/mieweb/pulse) `pages/`), which sends the person to the store. Details stay after `#`, so GitHub never sees them.
- Keep `.nojekyll` at the root, or this folder isn't published.
