---
layout: default
title: Core Concepts
nav_order: 3
---

## Core Concepts

### App

The `App` class is the entry point of your application. It initializes the terminal, handles input events, and manages the main event loop.

```cpp
#include "cpptui.hpp"
using namespace cpptui;

int main() {
    App app;
    auto root = std::make_shared<Vertical>();
    // ... add widgets to root ...
    app.run(root);
    return 0;
}
```

- **Graceful Exit**: `App::quit()` can be called to exit the event loop and restore the terminal state.
- **Exit Keys**: `register_exit_key(int key, bool ctrl=false, bool alt=false, bool shift=false)` adds a key that will trigger application exit.
- **Timers**:
  - `add_timer(interval_ms, callback)`: Schedule a repeating callback. Returns a `TimerId`.
  - `remove_timer(timer_id)`: Stop and remove a timer.
- **Dialogs**:
  - `open_dialog(dialog)`: Opens a dialog auto-centered on screen.
  - `open_dialog(dialog, x, y)`: Opens a dialog at specific coordinates.
  - `close_dialog(dialog)`: Closes the specified dialog.

### Widget

Every visual element in cpp-tui inherits from the `Widget` class. Widgets have:
- **Geometry**: `x`, `y`, `width`, `height`.
- **Sizing Policy**: `fixed_width`, `fixed_height` (0 or negative means flexible).
- **Rendering**: `render(Buffer& buffer)` method to draw to the screen.
- **Visibility**: `visible` property to show/hide.
- **Responsive Width**: `set_responsive(sm, md, lg)` or `set_responsive_width(sm, md, lg)` to auto-toggle based on screen width.
- **Responsive Height**: `set_responsive_height(sm, md, lg)` to auto-toggle based on screen height.
- **Events**: `on_click`, `on_key`, `on_hover`, etc.
- **Focus**: `set_focus(bool)` to manually set focus, `has_focus()` to check state.
- **Tab Navigation**: `tab_stop` (bool) determines if the widget is included in Tab cycle.
- **Hover**: `on_hover(bool)` callback triggered when mouse enters/exits.
- **Tooltips**:
  - `set_tooltip(text)`: Quickly attach a text tooltip.
  - `set_tooltip(std::shared_ptr<Tooltip>)`: Attach a custom or shared `Tooltip` instance.

### Theme

The `Theme` class manages the color palette of the application.

- **Set Theme**: `Theme::set_theme(Theme::Dark())` or any built-in theme.
- **Built-in Themes**:
  - `Theme::Dark()` - Catppuccin Mocha (soothing pastel dark theme)
  - `Theme::Light()` - Catppuccin Latte (soothing pastel light theme)
  - `Theme::Nord()` - Arctic, north-bluish color palette
  - `Theme::TokyoNight()` - Modern dark theme inspired by Tokyo's nightscape
  - `Theme::SolarizedLight()` - Classic scientific color palette by Ethan Schoonover
- **Custom Theme**: You can create a `Theme` struct and assign custom `Color` values (including `scrollbar_track`, `input_placeholder`, etc).

### Events

Events are handled by the `App` and propagated to widgets.
- **Key Events**: Pressing keys like `Enter`, `Esc`, `Tab`, or arrow keys.
- **Mouse Events**: Clicks, drags, and scrolling.
- **Focus**: `Tab` / `Shift+Tab` cycles focus between interactive widgets.
- **Resize**: `g_resize_pending` signal handling for terminal resize events.

### Clipboard & History

Global default keybindings are available for text editing widgets (`Input`, `TextArea`, and selectable `Label`).
- **Copy**: `Ctrl+C` or `Ctrl+Shift+C`
- **Cut**: `Ctrl+X` or `Ctrl+Shift+X` (Editable widgets only)
- **Paste**: `Ctrl+V` or `Ctrl+Shift+V` (Editable widgets only)
- **Undo**: `Ctrl+Z` (Editable widgets only)
- **Redo**: `Ctrl+Shift+Z` or `Ctrl+Y` (Editable widgets only)
- **Select All**: `Ctrl+A` or **Triple-click**
