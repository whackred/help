# The manifest format

This section describes the manifest format file `whack_red.toml`, placed at a project's root directory.

A manifest may describe a package and a workspace simultaneously.

## Example

```toml
[package]
name = "me.matt.eval"
version = "0.1.0"
runtime = "http://www.w3.org/1994/web"

[compiler-options]
main-class = "me.matt.eval.Main"
```

## Package section

```toml
[package]
# The package ID.
#
# Patterns (may use subnamespaces):
#
# - `com.<company>.<project-name>`
# - `org.<organisation>.<project-name>`
# - `net.<organisation>.<project-name>`
# - `me.<author>.<project-name>`
# - `goog.<project-name>`
# - `<project-name>`
#
name = "com.company.project-name"

# SemVer-compatible version number.
#
version = "0.1.0"

# Target platform.
#
# Supported values:
#
# - "http://www.w3.org/1994/generic"
#   - Compatible with web and NodeJS.
# - "http://www.w3.org/1994/web" (web browser)
# - "http://www.nodejs.org/2009" (NodeJS)
#
runtime = "http://www.w3.org/1994/javascript"

# Author list.
#
authors = ["matt <me@matt.me>"]

# Homepage URL.
#
homepage = "https://project.com"

# Source repository URL.
#
repository = "https://github/example/project"

# License type.
#
# Examples:
#
# "MIT", "Apache-2.0", "MIT OR Apache-2.0"
#
license = "MIT OR Apache-2.0"

# Description.
#
description = "Package description."

# Keywords.
#
keywords = []

# Categories.
#
categories = []

# Files to exclude/include when publishing.
# (Similiar to .gitignore entries, possibly with an exclamation prefix.)
#
ignore = []

# Shared objects (.so or .dll) to contribute alongside
# the program. This may be used when creating
# native applications, by combining the Tauri technology
# with client-side Whack Red.
#
# Entries in this option can interpolate `{target}`
# for the arfifact directory.
#
# Entries not found here are ignored; for instance,
# you could have a .dll on Windows, but not on other platforms.
#
shared-objects = [
    "{target}/so/org.makers.plus/libcore.so",
]

# Plain metadata ignored by Whack Red
[package.metadata]
plain = 0
```

## Workspace section

```toml
[workspace]
members = [
    "packages/foo",
    "packages/bar",
]
```

## Dependencies sections

```toml
# Dependencies.
#
[dependencies]
me.matt.foo = "0.1"
me.matt.bar = { path = "../bar", version = "0.1" }
# git dependencies may have a `rev`, `tag` or `branch` keys.
#
# rev examples:
#
# - rev = "4c59b707" (a commit by its SHA1 hash)
# - rev = "refs/pull/493/head" (HEAD commit of PR 493)
#
# tag examples:
#
# - tag = "1.10.3"
#
# branch examples:
#
# - branch = "master"
#
# If it's a workspace, then Whack Red will look for the
# matching member, inheriting any dependencies.
#
me.matt.qux = { git = "https://github.com/matt/qux", version = "0.1" }

# Development dependencies. *Used by unit-testing.*
#
[dev-dependencies]
com.alpha.lets-go = "1"

# Build dependencies. *Used by build scripts.*
#
[build-dependencies]
com.omega.game = "1"

# NPM dependencies, for internal use
# in Whack Red facade packages.
#
[npm-dependencies]
"decimal.js" = "1"
```

## Compiler options section

```toml
[compiler-options]
# Directory at which to find ShockScript source files.
# (Defaults to "src".)
#
source-path = "src"

# Main component or class, for an application package.
#
main-component = "me.matt.eval.Main"

# following: "error", "warn" or "allow"
unreachable-code = "warn"
unused = "warn"
```

## Terminal section

Used for contributing terminal applications, installable through `whackred terminal install`.

```toml
[[terminal]]
name = "mycmd1"
main-class = "me.matt.eval.terminal.MyCommand1"

[[terminal]]
name = "mycmd2"
main-class = "me.matt.eval.terminal.MyCommand2"
```

## Unit-testing sections

```toml
[[test]]
# Test ID.
#
# This may be omitted if there is only one [[test]]
# section, defaulting to "test".
#
# This is required internally.
name = "test"

# Runtime. Accepts the same values as `application.runtime`.
#
# Defaults to "http://www.nodejs.org/2009".
#
runtime = "http://www.nodejs.org/2009"

# Directory at which to find ShockScript unit-testing source files.
#
# Defaults to "test" if there is only one [[test]] section.
#
source-path = "test/es4"
```

If there is no `[[test]]` section and there is a `test` directory, then a virtual `[[test]]` section is added with the default options.

## Formatting section

```toml
[formatting]
# Number of spaces per indentation-level.
#
# Default: 4
tab-width = 4

# Use tabs for indentation?
#
# Default: false
use-tabs = false

# Insert semicolons after statements?
#
# Default: true
#
semicolon = true

# Use single quote strings were appropriate?
#
# Default: false
#
single-quote = false
```

## Application section

The `application` section is reserved for visual-interactive application frameworks.

```toml
[application]
# Human name (`en` is the default locale).
human-name."en" = "Application 1"
human-name."pt" = "Aplicativo 1"
# Description
description."en" = "Description"
description."pt" = "Descrição"
# Frames per second.
framerate = 30
# Background color.
background = "#fff"
# App-installation resources directory.
#
# This is used by the `app:` scheme for resolving
# assets from the app's installation directory.
#
# Default: res.
#
resources = "res"

# For web projects, indicates the
# absolute path of the web project in its host.
#
wwwroot = "/"

[application.initial-window]
# Window size
width = 800
height = 600
```