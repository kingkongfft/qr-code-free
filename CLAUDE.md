# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-file QR Code Generator built for the EPAM APAC Wellness Week 2026 event. Zero dependencies, no build step — open `qr-code.html` directly in a browser to run it.

## Running the Project

No build or install step. Open `qr-code.html` in any modern browser.

## Architecture

The entire application lives in one file: `qr-code.html`, organized in three sections:

1. **`<style>` block (in `<head>`)** — All CSS. Uses CSS custom properties for the dark-mode palette, an animated radial gradient background via `body::before`/`body::after` pseudo-elements, and glassmorphism on the card. Single responsive breakpoint at `max-width: 640px`.

2. **`<body>`** — A centered `.container` card with a URL text input (`#urlInput`, wired to `oninput="generateQR()"`), a `#qrcode` div where the library injects a `<canvas>`, and a download button.

3. **`<script>` block (bottom of `<body>`)** — Three functions:
   - `generateQR()` — Clears `#qrcode`, creates a new `QRCode` instance (280×280 px, error-correction level H), updates `#urlDisplay`.
   - `downloadQR()` — Reads the `<canvas>` via `toDataURL()` and triggers a PNG download.
   - `window.addEventListener('load', ...)` — Fires `generateQR()` after 100 ms to render the default URL on page load.

## External Dependencies (CDN only)

- **QR library:** `qrcodejs 1.0.0` from cdnjs — loaded at the bottom of `<body>`, provides the `QRCode` constructor.
- **Fonts:** Google Fonts (Outfit, Space Grotesk).
- There is also a dead `<script>` tag in `<head>` loading `qrcode@1.5.3` from jsDelivr — this is unused and can be safely removed.

The page requires internet access for the CDN library and fonts to function.
