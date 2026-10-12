# mieweb.github.io

The root of `https://mieweb.github.io/`, mieweb's organization site. Project sites (like `/pulse/`) are published from their own repos.

## App links

- `.well-known/` lets `https://mieweb.github.io/...` links open mieweb's mobile apps. Phones only read it at the domain root, which only this repo can serve.
- **Pulse** uses it so a pairing link (`/pulse/open#…`) opens the app directly when installed. See [`.well-known/README.md`](.well-known/README.md).
- Never set a custom domain here: the redirect stops these links from opening apps.
