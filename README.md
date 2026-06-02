# jbrowse-plugin-esbuild-template

JBrowse 2 plugin template using esbuild, pnpm, vitest, and ESLint flat config.

## Setup

Via GitHub CLI:

```console
gh repo create jbrowse-plugin-my-project --template GMOD/jbrowse-plugin-esbuild-template
cd jbrowse-plugin-my-project
pnpm install
```

Or clone manually:

```console
git clone https://github.com/GMOD/jbrowse-plugin-esbuild-template jbrowse-plugin-my-project
cd jbrowse-plugin-my-project
rm -rf .git && git init
pnpm install
```

### Renaming the plugin

The plugin name appears in several places that must all stay in sync:

| File | What to change |
|---|---|
| `package.json` | `name` field |
| `esbuild.mjs` | `globalName` and `outfile` |
| `src/index.ts` | class name and `name` field |
| `config.json` | plugin `name` and `url` |

## Development

```console
pnpm dev  # builds and serves on port 9000 with CORS headers
```

Point JBrowse Web at: `http://localhost:3000/?config=http://localhost:9000/config.json`

## Build

```console
pnpm build  # outputs dist/jbrowse-plugin-template.umd.production.min.js
```

## Testing

```console
pnpm test       # unit tests (jsdom + React Testing Library)
pnpm test:e2e   # puppeteer against nightly JBrowse (downloads on first run)
```

## Deployment

There are many ways to deploy — some options:

- **npm** — set `"private": false` and `pnpm publish` (consider [npm trusted publishing](https://docs.npmjs.com/generating-provenance-statements)); reference via unpkg:
  ```json
  { "plugins": [{ "name": "MyPlugin", "url": "https://unpkg.com/jbrowse-plugin-my-project/dist/jbrowse-plugin-my-project.umd.production.min.js" }] }
  ```
- **Copy the bundle** — run `pnpm build` and place the `.umd.production.min.js` file anywhere your JBrowse instance can reach it, then reference it by URL in `config.json`.
- **Skip publishing** — for internal or single-instance use, just serve `dist/out.js` locally and point your JBrowse config at it.

---

See [jbrowse-plugin-gwas](https://github.com/cmdcolin/jbrowse-plugin-gwas) for a real-world example using this setup.
