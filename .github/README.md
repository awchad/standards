# Introduction

**This document is inspired by LLVM code standards.**

This document describes the coding standards used in the AwChad project. While no coding standards should be considered an absolute requirement to be followed in all instances, coding standards are particularly important for large-scale codebases.

### Languages, Libraries and Standards.

Most of the source code in AwChad projects using these coding standards is Lua code. Generally, our preference is for clean, readable Lua code by standards.

> **TEMPORARY MESSAGE**: *While we are only working on configuring AwesomeWM, there will only be code conventions for Lua code.*

# Code Conventions for Lua

## Source Code Formatting

### Commenting

Comments are important for readability and maintainability. When writing comments, write them as English prose, using proper capitalization, punctuation, etc. Aim to describe what the code is trying to do and why, not how it does it at a micro level. Here are a few important things to document:

#### File Headers

Every source file should have a header on it that describes the basic purpose of the file. The standard header looks like this:

```lua
-- !!! awchad/object.lua - Object class definition ......... -*- Lua -*- !!!
--
-- Part of AwChad project, under the GNU General Public License v3.
-- See https://www.gnu.org/licenses/gpl-3.0.en.html for license information.
-- SPDX-License-Identifier: GPL-3.0-only
--
-- !!! ................................................................. !!!
---
--- The base class for object-oriented programming used by various
--- components of AwChad.
---
-- !!! ................................................................. !!!
```

A few things to note about this particular format: The string `-*- Lua -*-` on the first line is there to tell Emacs that the source file is a Lua file. (Even though Emacs knows that a `.lua` file is Lua code, this is a convention).

The next section of the file is a concise note that defines the license under which the file is released. This makes it perfectly clear on what terms the source code can be distributed and must not be modified in any way.

The main body is a [EmmyLua](https://emmylua.github.io/) comment (identified by the `---` comment marker instead of the usual `--`) describing the purpose of the file.

#### EmmyLua

EmmyLua annotations like classes, fields and aliases whenever possible stay under the header section of the file:

```lua
-- !!! ..... EmmyLua Section ..... !!! --

--- Describes the person's information.
--- @class CtorPersonDescriptor
--- @field name string The person's name.
--- @field age integer The person's age.
--- @field city string Where the person lives.

--- @alias ClientSignal
--- | "focus" # Emitted when a client gains focus..
--- | "unfocus" # Emitted when a client gets unfocused.

-- !!! ........................... !!! --
```

#### Documentation Comments

In general, prefer to use `---` instead of `--` when documenting code.

Include descriptive paragraphs for all public interfaces (public classes, member and non-member functions). Avoid restating information that can be inferred from the API name. The first sentence is used as a summary. Put the detailed discussion in separate paragraphs.

A minimal documentation comment:

```lua
--- Play a sound file.
---
--- @param path string The file path.
function play_sound(path) end
```

A documentation comment that uses more EmmyLua features:

```lua
--- Measures the text size.
---
--- Size may vary depending on font settings.
---
--- Usage:
--- ```
--- local draw_width = measure_width('Hello, world!', {
---   family = 'JetBrains Mono',
---   weight = 400,
---   size = 14,
--- })
--- ```
---
--- @param text string The text to be measured.
--- @param font FontDescriptor Text font settings.
function measure_width(text, font)
```

Do not duplicate the documentation comment in the header file and implementation file. Place documentation comments for public APIs in the header file. Documentation comments for private APIs can go to the implementation file. In any case, implementation files can include additional comments to explain implementation details as needed.
