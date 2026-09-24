# Markdown Studio

Markdown Studio is a self-contained, offline visual editor for normal Markdown files. It was built for working with configuration cheatsheets and notes on isolated networks, where a web service, CDN, or running server should not be required.

## Live site

Try Markdown Studio at [mdstudio.saltyoldgeek.com](https://mdstudio.saltyoldgeek.com).

## What it does

- Opens and saves `.md` files.
- Renders GitHub-Flavored Markdown locally through the embedded `gfm-wasm` WebAssembly renderer.
- Supports code blocks, editable Mermaid-style system flowcharts, and local file/folder workflows where the browser permits them.
- Keeps an encrypted browser-local draft using Web Crypto AES-GCM and a non-extractable IndexedDB key.
- Runs directly from disk with `file://`; it does not require installation or a server.

## Use

Download or clone the repository, then open `Markdown Studio v2.html` in a modern browser.

Some browser File System Access API features, such as direct folder browsing and save-back, may require a Chromium-based browser and an HTTPS origin. The core editor and explicit download/save workflow remain usable directly under `file://`.

## Security and dependencies

The active HTML file has no CDN loader, runtime network calls, external scripts, `fetch`, XHR, or WebSocket requirement.

`package.json` and `package-lock.json` intentionally declare the single embedded third-party dependency, `gfm-wasm` 1.0.1. This allows GitHub's dependency graph and Dependabot tooling to evaluate the dependency accurately. The embedded `dist/cmark.wasm` asset was verified against the upstream package with SHA-256:

```text
c2215cf1010f6cd84324d6dae1bbe25cd52732b4f4aa7a519387b234a46f128e
```

The Mermaid-style flowchart renderer is local project code, not the Mermaid package. It intentionally accepts only a constrained flowchart subset and rejects directives, click actions, links, style/class commands, and unsupported diagram types.

Browser-local draft encryption protects against casual inspection of browser storage. It does not protect against someone operating in the same unlocked browser profile, and it is not a replacement for full-disk encryption.

## License

Markdown Studio is released under the [MIT License](LICENSE).
