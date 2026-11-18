# Massai

**Massai** — a self-owned, DeepSeek-backed coding environment. It's an **overlay** on
[DSH](https://github.com/deepseek-ai/deepseek-harness) (MIT): clone upstream, apply this
repo, and you have Massai.

## What Massai adds (over upstream DSH)

| Feature | Where |
| --- | --- |
| **Auto-failover** — a retryable V4-Pro failure auto-retries on the cheaper Flash tier | `patches/massai-core.patch` |
| Cost-aware model routing (`route_model` tool: flash for simple, V4-Pro for complex) | `packages/experimental/model-router` |
| Per-user DeepSeek keys for a hosted link (each visitor's own key, own cost) | `packages/experimental/user-credentials` + core patch |
| `cai` — your DeepSeek coding agent as a DSH tool | `packages/experimental/tool-cai` |
| One-way `sync` (rclone, age-guarded) | `packages/experimental/tool-sync` |
| Embedded SQLite database (`db_exec` / `db_query`) | `packages/experimental/tool-sqlite` |
| Generic HTTP requests (vault-credential auth) | `packages/experimental/tool-http` |
| Account connectors (vault) | `packages/experimental/account-connect` |
| `massai` (default) + `cheap` agent presets, cost-aware defaults | `packages/experimental/massai-bundle` |
| Hosted-link deployment | `Dockerfile` + `render.yaml` |
| Android APK shell (WebView, CI-built) | `mobile-apk/` |

## Build Massai

```bash
# 1. clone upstream DSH
git clone https://github.com/deepseek-ai/deepseek-harness.git
cd deepseek-harness

# 2. apply this overlay
cp -r /path/to/massai/packages/experimental/* packages/experimental/
git apply /path/to/massai/patches/massai-core.patch
# copy Dockerfile, render.yaml, mobile-apk/, .github/workflows/ as wanted

# 3. install + verify
corepack pnpm install --no-frozen-lockfile
corepack pnpm run typecheck
corepack pnpm run build
```

## DeepSeek backbone

Massai runs on **your own DeepSeek account** — V4-Pro (flagship coder) and Flash
(cheap tier). Sign in with your DeepSeek API key: your key, your cost, your usage.

## Naming

"Massai" is the product name. Describe the lineage as "built on DSH" / "a fork of DSH"
(per upstream's brand guidelines).

## License

MIT (this overlay). Upstream DSH is MIT © DeepSeek.
