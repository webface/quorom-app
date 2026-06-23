# Quorom

**Your private AI cluster, reachable from anywhere.**

Quorom turns the machines you already own into one OpenAI-compatible
inference cluster — without Tailscale invites, port forwarding, or
distributed-inference complexity.

---

## Download

| Platform | Link |
|---|---|
| macOS (universal) | [quorom-macos-universal.zip](https://github.com/webface/quorom-app/releases/latest/download/quorom-macos-universal.zip) |
| Windows (amd64) | [quorom-windows-amd64.exe](https://github.com/webface/quorom-app/releases/latest/download/quorom-windows-amd64.exe) |

Linux builds coming soon.

## Install

### macOS
1. Download and unzip `quorom-macos-universal.zip`
2. Drag `Quorom.app` to `/Applications`
3. Right-click → **Open** the first time (to bypass Gatekeeper — the app is self-signed)

### Windows
1. Download `quorom-windows-amd64.exe`
2. If SmartScreen warns about an unknown publisher, click **Run anyway**
3. The app runs from wherever you saved it; no installer required

---

## What it does

- **Zero-config networking.** Nodes connect outbound to the Quorom relay. No firewalls to open, no port forwarding, no invite ACLs.
- **OpenAI-compatible.** Point Cursor, Open WebUI, or curl at `https://api.quorom.app/v1` — it drops in anywhere the OpenAI SDK is used.
- **Use your own hardware.** Your machines' GPUs and RAM become cluster nodes. No model duplication.
- **Local-first.** Models run on hardware you control. The relay only brokers metadata and token streams; it never stores prompts or completions.

## Quick start

1. Download and launch Quorom
2. Follow the setup wizard (auto-detects Ollama, offers one-click install + model pull)
3. **Settings → Cloud Cluster → Sign in** to connect to the relay
4. Visit the [web dashboard](https://app.quorom.app) to create a cluster and generate an API key
5. Share the cluster invite code with anyone you want to join
6. Use it from anywhere:

```bash
curl https://api.quorom.app/v1/chat/completions \
  -H "X-Quorom-Cluster: <invite-code>" \
  -H "X-Quorom-API-Key: <api-key>" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "llama3.1:8b",
    "messages": [{"role":"user","content":"hello"}],
    "stream": true
  }'
```

## Backends supported

Each node can serve inference from any of:
- **Ollama** (auto-installer in the wizard)
- **LM Studio** (Local Server)
- **llama.cpp** `llama-server`
- **MLX** on Apple Silicon
- **vLLM**
- Any other **OpenAI-compatible** HTTP server
- Built-in **Mock engine** for testing without any model software

## Status

Quorom is in **alpha**. Things may break. Token-streaming is stable; the desktop UI and web dashboard are evolving.

- ✅ Cross-platform desktop app (macOS, Windows)
- ✅ Relay-routed cluster networking
- ✅ OpenAI-compatible API
- ✅ Clerk-based authentication
- ✅ Convex-backed cluster state
- 🚧 Linux desktop builds
- 🚧 In-app auto-update
- 🚧 Per-cluster usage billing
- 🚧 Team / org management

## Privacy

Quorom is designed to be **local-first**. Your prompts and completions
never touch the relay in persisted form — the relay forwards token
streams in memory and discards them. The only data persisted to Convex
is:
- Your email and Clerk user ID (for auth)
- Node display names + the list of models each node is serving
- Aggregate usage counters (tokens in/out per request, for metering)

Read the full [Privacy Policy](https://app.quorom.app/privacy) and
[Terms of Service](https://app.quorom.app/terms).

## Pricing

Free during alpha. Eventual pricing will be relay-bandwidth based; local
inference on your own hardware will always be free.

## Issues

File bugs and feature requests in this repo's [Issues](https://github.com/webface/quorom-app/issues).

## License

The Quorom app binaries are © 2026 Webfacemedia Inc. and provided free
of charge during the alpha period. Source code is currently proprietary.
