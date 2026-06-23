<p align="center">
  <img src="og.png" alt="Quorom — Your private AI cluster, reachable from anywhere." width="600">
</p>

<h1 align="center">Quorom</h1>

<p align="center">
  <strong>Your private AI cluster, reachable from anywhere.</strong>
</p>

<p align="center">
  <a href="https://github.com/webface/quorom-app/releases/latest">Download</a> ·
  <a href="https://app.quorom.app/install">Install Guide</a> ·
  <a href="https://app.quorom.app/dashboard">Dashboard</a> ·
  <a href="https://app.quorom.app/terms">Terms</a> ·
  <a href="https://app.quorom.app/privacy">Privacy</a>
</p>

---

Quorom turns the machines you already own into one OpenAI-compatible
inference cluster — without VPNs, port forwarding, or networking headaches.

---

## Download

| Platform | Link |
|---|---|
| macOS (universal) | [quorom-macos-universal.zip](https://github.com/webface/quorom-app/releases/latest) |
| macOS (installer) | [quorom-macos-installer.dmg](https://github.com/webface/quorom-app/releases/latest) |
| Windows (amd64) | [quorom-windows-amd64.exe](https://github.com/webface/quorom-app/releases/latest) |

Need help? See the [Install Guide](https://app.quorom.app/install).

## Install

### macOS
1. Download the `.dmg`, open it, drag **Quorom.app** to **Applications**
2. First launch: bypass Gatekeeper — run in Terminal:
   ```
   xattr -dr com.apple.quarantine /Applications/Quorom.app
   ```
   Or: System Settings → Privacy & Security → "Quorom was blocked" → **Open Anyway**
3. Launch Quorom

### Windows
1. Download the `.exe`
2. Run it — if SmartScreen warns, click **More info** → **Run anyway**

---

## What it does

- **Zero-config networking.** Nodes connect outbound to the Quorom relay. No firewalls, no port forwarding, no network configuration.
- **OpenAI-compatible.** Point Cursor, Open WebUI, or curl at `https://api.quorom.app/v1` — it drops in anywhere the OpenAI SDK is used.
- **Use your own hardware.** Your machines' GPUs and RAM become cluster nodes. No model duplication.
- **Local-first.** Models run on hardware you control. The relay only brokers metadata and token streams — it never stores prompts or completions.
- **Distributed inference.** Split a model across machines so every node contributes compute to each token.

## Quick start

1. Download and launch Quorom
2. Follow the setup wizard (auto-detects Ollama / LM Studio, offers one-click install)
3. **Settings → Cloud Cluster → Sign in** to connect to the relay
4. Visit the [web dashboard](https://app.quorom.app) to create a cluster and get an invite code
5. Share the invite code with anyone you want to join
6. Use it from anywhere:

```bash
curl https://api.quorom.app/v1/chat/completions \
  -H "X-Quorom-Cluster: <invite-code>" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "llama3.1:8b",
    "messages": [{"role":"user","content":"hello"}],
    "stream": true
  }'
```

## Supported backends

Each node can serve inference from any of:
- **Ollama** (auto-installer in the wizard)
- **LM Studio** (Local Server)
- **llama.cpp** (including RPC for distributed inference)
- **MLX** on Apple Silicon
- **vLLM**
- Any other **OpenAI-compatible** HTTP server

## Status

Quorom is in **alpha**.

- ✅ Cross-platform desktop app (macOS, Windows)
- ✅ Relay-routed cluster networking
- ✅ OpenAI-compatible API
- ✅ Secure authentication
- ✅ Persistent cluster state
- ✅ Distributed inference (model sharding across machines)
- 🚧 Apple notarization + Windows code signing
- 🚧 Linux desktop builds
- 🚧 In-app auto-update
- 🚧 Per-cluster usage billing
- 🚧 Team / org management

## Privacy

Quorom is designed to be **local-first**. Your prompts and completions
never touch the relay in persisted form — the relay forwards token
streams in memory and discards them.

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
