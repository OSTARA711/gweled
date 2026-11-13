# GWELED

**A GTK4 document viewer**

GWELED is a GTK4-based document viewer derived from [Zathura](https://pwmt.org/projects/zathura/), originally developed by pwmt.org.

It retains Zathura's document-viewing architecture and plugin-based design while using GTK4 and a modernised Girara interface.

GWELED is designed to provide a lightweight, configurable document-viewing application with support for different document formats through external plugins.

## Features

- GTK4 graphical interface.
- Document opening through a graphical file chooser.
- Drag-and-drop document opening.
- Plugin-based document format support.
- Keyboard-oriented navigation and configurable controls inherited from Zathura.
- Page navigation, zooming and document layout controls.
- Persistent document state and bookmarks.
- Optional SyncTeX integration.
- Optional application sandboxing through seccomp and Landlock.

Document format support depends on the installed plugins. GWELED does not bundle a document-rendering backend into its core application.

## Architecture

GWELED separates the viewer from document-format implementations.

- **GWELED:** application, GTK4 interface, document lifecycle, navigation, rendering coordination and plugin API.
- **Girara:** user-interface support library.
- **Document plugins:** external implementations providing format-specific document loading, rendering and related operations.

This architecture allows document formats to be supported independently of the main application.

## Requirements

### Runtime and build dependencies

| Dependency | Minimum version | Purpose |
|---|---:|---|
| GTK4 | 4.18 | Graphical interface |
| GLib | 2.84 | Core application facilities |
| Girara | 2026.07.07 | User-interface library |
| JSON-GLib | — | JSON support |
| Cairo | — | Graphics |
| libmagic | — | MIME-type detection |
| SQLite | 3.35.0 | Document state database |
| libxxhash | — | File hashing |

A C23-compatible compiler is required.

### Build tools

- Meson 1.5 or newer
- Ninja (when using the Ninja backend)
- pkgconf
- gettext

### Optional dependencies

| Dependency | Purpose |
|---|---|
| SyncTeX (`libsynctex` 2 or newer) | TeX source synchronisation |
| libseccomp | seccomp-based sandboxing |
| Linux Landlock support | Filesystem sandboxing |

Optional documentation dependencies include Sphinx, Doxygen, Breathe and the Sphinx Read the Docs theme.

## Building

Configure the project:

```sh
meson setup build
```

Compile:

```sh
meson compile -C build
```

Install:

```sh
sudo meson install -C build
```

Refresh the shared-library cache where appropriate:

```sh
sudo ldconfig
```

Meson automatically selects an available build backend unless one is explicitly specified.

## Plugins

GWELED uses a versioned plugin interface.

Current versions:

- Plugin API: 8
- Plugin ABI: 9

Plugins must be built against a compatible GWELED installation. Plugins compiled for incompatible Zathura API or ABI versions cannot be assumed to work.

Document-format support is provided by separately maintained plugins.

## Project origins

GWELED is derived from Zathura, originally developed by pwmt.org.

The project retains the original upstream copyright and licensing notices. GWELED-specific modifications and original contributions are maintained separately.

## Licence

GWELED retains the original Zlib licence terms. See [LICENSE.md](LICENSE.md) for the complete licence text and copyright notices.

## Development

Source code:

https://github.com/OSTARA711/gweled

Bug reports and development discussions should be directed to the GWELED repository.
