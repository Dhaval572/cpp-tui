---
layout: default
title: Troubleshooting
nav_order: 5
---

## Troubleshooting

### Wide Characters Display Issues
cpp-tui has built-in support for wide characters including CJK (Chinese, Japanese, Korean) and emoji. The library correctly calculates display widths for:
- ASCII and Latin characters (1 cell wide)
- CJK Unified Ideographs, Hiragana, Katakana, Hangul (2 cells wide)
- Common emoji (2 cells wide)
- Combining diacritical marks (0 cells wide)

If you are experiencing display issues with wide characters, ensure:
1. Your terminal uses a monospace font with good Unicode support (e.g., **Consolas**, **DejaVu Sans Mono**, **JetBrains Mono**, **Noto Sans Mono CJK**)
2. Your terminal correctly renders wide characters as double-width

### Mouse Input Not Working
If mouse input is not being recognized by the application, check your terminal's mouse settings to ensure that mouse input is being passed through to applications. Some terminals have options like "Mouse Tracking" or "Send mouse events to application" that need to be enabled.

### Ambiguous Width Characters
Certain Unicode symbols (like `✓` U+2713, `⚠` U+26A0, `✗` U+2717) have "Ambiguous" width in the Unicode standard. Terminals may render them as single-width or double-width depending on fonts and configuration.
cpp-tui explicitly treats these common icon symbols as **Width 1 (Narrow)** to ensure consistent rendering layout across most terminals. If your terminal forcibly renders these as wide, you may see minor overlap artifacts.
