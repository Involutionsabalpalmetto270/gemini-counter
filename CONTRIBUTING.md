# Contributing to Gemini Counter

Thanks for your interest in contributing! Here's how to get involved.

## Getting Started

1. **Fork** the repo and clone your fork
2. Load the extension in Developer mode (`chrome://extensions` → Load unpacked → select `gemini_counter_v2/`)
3. Make your changes, reload the extension, and test on [gemini.google.com](https://gemini.google.com)

## What to Work On

- 🐛 **Bug reports** — Open an issue with steps to reproduce
- ✨ **New models** — Add missing Gemini models to `src/content/constants.js`
- 🎨 **UI improvements** — Widget styles are in `src/styles.css`
- 🧠 **Token logic** — Core counting lives in `src/content/tokens.js`

## Pull Request Guidelines

- Keep PRs focused — one fix or feature per PR
- Update the README if your change affects usage or the model table
- Test in Chrome before submitting
- Use clear commit messages: `fix: correct UTF-8 decoder flag` or `feat: add Gemini 2.5 Ultra model`

## Reporting Bugs

Please include:
- Browser and version
- Extension version
- Steps to reproduce
- What you expected vs. what happened
- Console errors (open DevTools → Console)

## Code Style

- Plain vanilla JS — no build step, no bundler
- Keep files small and focused (each file in `src/content/` has one job)
- Prefer `const` and arrow functions
- No external dependencies — the extension is intentionally self-contained

---

Thank you for helping make Gemini Counter better! 🙏
