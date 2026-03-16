---
layout: default
title: Home
nav_order: 1
---

## cpp-tui Documentation

**cpp-tui** is a lightweight, single-header C++ library for creating Text User Interfaces (TUIs). It uses modern C++17 features and provides a rich set of widgets and layout managers, similar to web or GUI frameworks.

### Quick Start

```cpp
#include "cpptui.hpp"
using namespace cpptui;

int main() {
    App app;
    Theme::set_theme(Theme::Dark());

    auto root = std::make_shared<Vertical>();
    root->add(std::make_shared<Label>("Hello, cpp-tui!"));
    root->add(std::make_shared<Button>("Click me", []() {
        // handle click
    }));

    app.run(root);
    return 0;
}
```

---

### Documentation

<div class="doc-cards">

<a class="doc-card" href="{{ '/getting-started' | relative_url }}">
<h3>🚀 Getting Started</h3>
<p>Install the library, compile your first app, and learn the basics in minutes.</p>
</a>

<a class="doc-card" href="{{ '/core-concepts' | relative_url }}">
<h3>📖 Core Concepts</h3>
<p>Understand the App lifecycle, Widget model, Theming, Events, and Clipboard support.</p>
</a>

<a class="doc-card" href="{{ '/api-reference' | relative_url }}">
<h3>📚 API Reference</h3>
<p>Complete reference for all widgets — Layouts, Containers, Inputs, Charts, Tables, and more.</p>
</a>

<a class="doc-card" href="{{ '/troubleshooting' | relative_url }}">
<h3>🔧 Troubleshooting</h3>
<p>Solutions for common issues — wide character display, mouse input, and Unicode pitfalls.</p>
</a>

</div>

---

### Feature Highlights

- **Single Header** — Drop `cpptui.hpp` into your project, no build system required
- **50+ Widgets** — Buttons, Inputs, Tables, Charts, TreeViews, Dialogs, and more
- **Layout System** — Vertical, Horizontal, Grid, SplitPane, scrollable containers
- **Built-in Themes** — Dark, Light, Nord, Tokyo Night, Solarized Light
- **Rich Interactivity** — Mouse support, focus management, keyboard navigation, clipboard
- **Unicode Ready** — Full CJK and emoji support with correct terminal width rendering
