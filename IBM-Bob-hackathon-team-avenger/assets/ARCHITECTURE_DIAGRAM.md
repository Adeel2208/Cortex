# Architecture Diagram

> Place `architecture-diagram.png` (or `.svg`) in this folder.
> The diagram source is embedded in `ARCHITECTURE.md` as Mermaid.

## How to export

### Option A — Mermaid CLI
```bash
npx @mermaid-js/mermaid-cli -i ARCHITECTURE.md -o assets/architecture-diagram.png
```

### Option B — VS Code
Open `ARCHITECTURE.md` in VS Code with the Mermaid Preview extension,
right-click the diagram → "Export as PNG" → save to `assets/architecture-diagram.png`.

### Option C — mermaid.live
1. Open https://mermaid.live
2. Paste the diagram from `ARCHITECTURE.md` (System Topology section)
3. Download as PNG → save here

## Diagram description (text fallback)

```
┌──────────────────────────────────────────────────────────────┐
│  cortex-api  (Python 3.11 · FastAPI + MCP SDK · port 8080)   │
│  MCP tools:    diary_save · diary_recall · diary_link_code   │
│                diary_feedback · diary_timeline               │
│  Storage  :    SQLite + sqlite-vec  (single-file, local)     │
│  Embeddings:   watsonx.ai (primary) · MiniLM-L6-v2 (local)  │
│  Transports:   stdio (Bob)  +  HTTP/SSE (bot, web, mobile)   │
└──────────────────────────────────────────────────────────────┘
        ▲ MCP/stdio              ▲ HTTP                ▲ HTTP
┌────────────────┐    ┌─────────────────────┐   ┌──────────────────┐
│  IBM Bob       │    │   cortex-bot        │   │  cortex-web      │
│  📓 mode +     │    │   Telegram          │   │  React + Vite +  │
│  skill + cmds  │    │   IBM STT or        │   │  TS + Carbon     │
│  + rules + MCP │    │   Whisper fallback  │   │  port 8081       │
└────────────────┘    └─────────────────────┘   └──────────────────┘
                                                         ▲ HTTP
                                               ┌──────────────────┐
                                               │  cortex-mobile   │
                                               │  Expo React      │
                                               │  Native (iOS/    │
                                               │  Android/Web)    │
                                               └──────────────────┘
```
