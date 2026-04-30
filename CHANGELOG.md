# Changelog

All notable changes to Gemini Counter are documented here.

---

## [2.0.0] — 2026-04-30

### Fixed
- **UTF-8 corruption** — `TextDecoder` was called twice on the same chunk with conflicting `stream` flags. Now uses a single decoder with `{ stream: true }` and a final flush.
- **postMessage origin** — All `window.postMessage` calls now target `window.location.origin` instead of `'*'`, preventing metadata leaking to cross-origin iframes.
- **Ghost duplicate widget** — `attach()` now removes the container from its current parent before re-inserting, preventing two counter widgets after DOM rebuilds.
- **DOM observer debounce** — `MutationObserver` on `document.body` now debounced 200ms to avoid unnecessary layout thrashing on Gemini's SPA.
- **Dead hash API** — Removed unused `kind: 'hash'` request handler from `bridge.js`.
- **`accumulatedText` variable** — Removed dead variable from stream handler.

### Added
- **Output token display** — `candidatesTokenCount` now shown in the UI as `N out`.
- **Tiered warning states** — Bar and token text have three states: normal → orange at 75% → red at 90%+.
- **Bar threshold markers** — Subtle tick marks on the progress bar at 75% and 90%.
- **Dynamic tooltip** — Token group tooltip shows live % context usage.
- **Unknown model logging** — Unrecognized models now log a console warning with the detected model string.
- **Conversation history storage** — Token counts persisted to `chrome.storage.local` (last 50 entries per conversation).
- **`gemini-2.5-flash-lite`** added to known models list.

---

## [1.0.0] — Initial Release

- Basic token count display on gemini.google.com
- Context bar showing prompt token usage
- Local `o200k_base` tokenizer fallback
- Known Gemini model context window limits
