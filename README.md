# 🔢 Gemini Counter v2.0.0

> A lightweight Chrome extension that shows **exact token counts**, a live context bar, output tokens, and model info — right inside [gemini.google.com](https://gemini.google.com).

![Gemini Counter in action](assets/screenshot.png)

---

## ✨ Features

- **Exact token counts** — pulled directly from Gemini's own `usageMetadata`, not a guess
- **Live context bar** — visual progress bar with tiered warning states (75% → orange, 90%+ → red)
- **Output tokens** — shows `N out` alongside prompt token count
- **Threshold markers** — subtle tick marks at 75% and 90% on the context bar
- **Dynamic tooltip** — live % context usage on hover
- **Conversation history** — token counts persisted per-conversation via `chrome.storage.local`
- **Model info** — detects and displays the active Gemini model
- **Fallback tokenizer** — uses a local `o200k_base` estimate before the first real response arrives

---

## 📸 Screenshot

The counter widget appears in Gemini's input bar, showing estimated input tokens, a progress bar, and the active model — all without leaving the page.

<img width="1280" height="226" alt="Screenshot 2026-04-30 at 1 34 42 PM Large" src="https://github.com/user-attachments/assets/4acdb5ef-2804-4beb-9c5d-40752258bb12" />



---

## 🚀 Installation

> Works on **Chrome**, **Edge**, and **Arc** (any Chromium-based browser).

1. **Download** this repo — click `Code → Download ZIP` or `git clone`
2. Open `chrome://extensions` in your browser
3. Enable **Developer mode** (toggle in the top-right)
4. Click **Load unpacked** and select the `gemini_counter_v2` folder
5. Navigate to [gemini.google.com](https://gemini.google.com) — the counter appears automatically ✅

---

## 🛠 How It Works

Gemini's web app uses internal, obfuscated endpoints (unlike Claude's clean REST API). This extension works around that by:

1. **Injecting a bridge script** into the page context to intercept `fetch` and `XMLHttpRequest`
2. **Parsing JSON response bodies** to find `usageMetadata` — the same data Google's official API returns
3. **Extracting** `promptTokenCount`, `candidatesTokenCount`, and `thoughtsTokenCount` directly
4. **Falling back** to a local tokenizer estimate until the first real API response arrives

Token counts come straight from Gemini — so they're **exact**, not estimated.

---

## 🔒 Privacy

- All data stays **local** — no external servers, no analytics, no tracking
- Only reads Gemini's own response data from your browser session
- Makes **zero** additional network requests
- Token history stored only in `chrome.storage.local`

---

## 📐 Context Window Limits

| Model | Context Window |
|---|---|
| Gemini 2.5 Pro | 1,048,576 tokens (1M) |
| Gemini 2.5 Flash | 1,048,576 tokens (1M) |
| Gemini 2.5 Flash Lite | 1,048,576 tokens (1M) |
| Gemini 2.0 Flash | 1,048,576 tokens (1M) |
| Gemini 1.5 Pro | 2,097,152 tokens (2M) |
| Gemini 1.5 Flash | 1,048,576 tokens (1M) |

Unknown models fall back to 1M and log a warning to the browser console.

---

## 📁 Project Structure

```
gemini_counter_v2/
├── manifest.json               # Extension manifest (MV3)
├── icons/
│   ├── icon16.png
│   ├── icon48.png
│   └── icon128.png
├── assets/
│   └── screenshot.png          # UI screenshot
└── src/
    ├── styles.css              # Counter widget styles
    ├── vendor/
    │   └── o200k_base.js       # Local tokenizer fallback
    ├── injected/
    │   └── bridge.js           # Page-context fetch interceptor
    └── content/
        ├── constants.js        # Model limits & config
        ├── bridge-client.js    # Messaging between contexts
        ├── tokens.js           # Token counting logic
        ├── ui.js               # Widget rendering
        └── main.js             # Entry point & orchestration
```

---

## 🆕 What's New in v2.0.0

### Bug Fixes
- **UTF-8 corruption fix** — `TextDecoder` now uses a single decoder with correct `{ stream: true }` flag, preventing multi-byte character corruption at chunk boundaries
- **postMessage origin hardened** — All `window.postMessage` calls target `window.location.origin` instead of `'*'`
- **Ghost duplicate widget fixed** — `attach()` removes the container from its current parent before re-inserting
- **DOM observer debounced** — `MutationObserver` debounced 200ms to avoid layout thrashing on Gemini's SPA
- **Dead hash API removed** — Unused `kind: 'hash'` handler removed from `bridge.js`
- **`accumulatedText` dead variable removed** — Cleaned up unused stream handler variable

### New Features
- Output token display (`N out`)
- Tiered warning states (normal → orange at 75% → red at 90%+)
- Bar threshold markers at 75% and 90%
- Dynamic tooltip with live % context usage
- Unknown model console warnings
- Conversation history storage (last 50 entries per conversation)
- `gemini-2.5-flash-lite` added to known models

---

## 🤝 Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a PR.

---

## 📄 License

[MIT](LICENSE) — free to use, modify, and distribute.
