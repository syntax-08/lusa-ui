# lusa-ui - terminal interface kit for Lusa

A TUI (terminal UI) library for the [Lusa programming language](https://github.com/syntax-08/lusa).
Everything is built from plain strings + ANSI escapes: colors, boxes, progress
bars, buttons. No native dependencies.

## Install

```cmd
lusalang install syntax-08/lusa-ui
```

Packages install into `%LOCALAPPDATA%\Lusa\packages` and are available to
every Lusa program on the machine via `require("ui")`.

## Usage

```lusa
local ui = require("ui")

print(ui.clear())
print(ui.box(2, 1, 58, 12, " my app "))
print(ui.text(4, 3, "hello from lusa-ui", 14))
print(ui.progress(4, 5, 30, 72))
print(ui.button(4, 7, "  click  ", 4))
print(ui.position(1, 14))
```

Run the bundled demo:

```cmd
lusa run demo.lusa
```

## API

| Function                              | Effect                                        |
| ------------------------------------- | --------------------------------------------- |
| `ui.clear()`                          | clear screen + home cursor                    |
| `ui.position(x, y)`                   | move cursor to column x, row y (1-based)      |
| `ui.fg(n)` / `ui.bg(n)`               | color escape (0-7 normal, 8-15 bright)        |
| `ui.reset()`                          | reset all attributes                          |
| `ui.paint(text, fg, bg)`              | pre-colored inline text                       |
| `ui.hline(width, ch?)`                | repeating line (`-` by default)               |
| `ui.text(x, y, str, fg?)`             | absolute-positioned colored text              |
| `ui.box(x, y, w, h, title?)`          | single-line box frame                         |
| `ui.progress(x, y, width, percent)`   | `████░░░░` progress bar                       |
| `ui.button(x, y, label, color?)`      | painted label (visual button)                 |

All functions **return strings** — nothing prints by itself. Compose and print.

## Notes

- Requires a terminal that renders ANSI escape codes (Windows Terminal,
  PowerShell, CMD on Win10+, macOS/Linux terminals).
- Ownership reminder: exported functions are cloned by the module, so
  `local ui = require("ui")` then `ui.text(...)` is safe to call repeatedly.

## License

MIT
