<p align="left">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/header-dark.png">
    <img src="assets/header-light.png" width="600" height="160" alt="Slideflow logo and name">
  </picture>
</p>

<p align="center"><b>Presentations and slide decks; a modern presentation and slide designer built in pure Rust.</b></p>

Slideflow is part of the FlowApps suite. It is an open-source presentation application: build decks
with themes, layouts, shapes, pictures, tables, charts, transitions and animations; open and save
.pptx files; present full screen. Native on macOS and Windows.

## Why Slideflow?

- **Free and open source** — MIT OR Apache-2.0
- **Your files** — open and save .pptx presentations; import PowerPoint 97–2003 .ppt/.pot/.pps
- **Themes & layouts** — slide masters, eleven layouts, eight themes with colour and font schemes
- **Draw & animate** — 150+ shapes, transitions, entrance/emphasis/exit animations, morph
- **Native desktop** — macOS (Apple Silicon) and Windows x64 builds
- **Private** — works offline; no accounts, no telemetry, no cloud

## Features

- **Build decks.** Slide masters, layouts with placeholders, sections, notes, comments, headers/footers.
- **Draw.** 150+ preset shapes, connectors, freeform, merge shapes, gradients, picture and pattern fills.
- **Write.** Full font and paragraph formatting, bullets, columns, autofit, vertical text, fields, hyperlinks.
- **Present.** Transitions (including Morph), animations, full-screen slide show, presenter view, rehearse timings.
- **Exchange files.** .pptx open/save, PDF/PNG/JPEG/GIF export.

## Download and install

Download the installer for your system (latest version, 0.1.0 release candidate 1). Slideflow is also available through the [FlowApps launcher](https://github.com/reachneoagent-commits/FlowApps-Launcher/releases/latest).

| Platform | Download |
|---|---|
| macOS, Apple silicon (M1 or newer) | [DMG](https://github.com/reachneoagent-commits/slideflow/releases/download/v0.1.0-rc.3/slideflow-0.1.0-rc.3-macos-arm64.dmg) |
| Windows x64 | [Portable zip](https://github.com/reachneoagent-commits/slideflow/releases/download/v0.1.0-rc.3/slideflow-0.1.0-rc.3-windows-x64-portable.zip) (unzip and run) |

macOS on Intel and a Windows installer are not built yet. Older versions and checksums are on the [Releases page](https://github.com/reachneoagent-commits/slideflow/releases).

The app is not code-signed with a paid certificate, so macOS and Windows warn you the first time you open it. Every release lists SHA-256 checksums to check the files against.

- **Mac:** open the DMG and drag Slideflow to Applications. Then right-click Slideflow, choose Open, and click Open again.
- **Windows:** if SmartScreen appears, click More info, then Run anyway.

## Supported platforms

- **Desktop app:** macOS on Apple Silicon; Windows x64 (Intel Mac build planned)

## Build from source

You need [Rust](https://rustup.rs/) 1.95+. Then run:

```bash
cargo build --release -p deckcraft
```

The desktop app binary is produced under `target/release/`.

## About this fork

Slideflow is based on [DeckCraft](https://github.com/storytold/deckcraft) by the ArtCraft team, rebranded as a FlowApps product. The original project is dual-licensed under MIT or Apache-2.0; that licensing is preserved here.

The ArtCraft name, wordmark and logos remain trademarks of the ArtCraft Team and are not used in Slideflow. Per the original NOTICE, forks and modified versions must remove them.

## Credits & Acknowledgments

Full third-party credits are in [`NOTICE`](NOTICE) and [`ATTRIBUTION.md`](ATTRIBUTION.md).

- **[DeckCraft](https://github.com/storytold/deckcraft)** by the ArtCraft team: the original presentation engine, UI and file formats (MIT OR Apache-2.0).
- **[craft-libs](https://github.com/storytold/craft-libs)** by the ArtCraft team: the shared UI framework and file-format libraries this app is built on, plus [egui](https://github.com/emilk/egui) (MIT OR Apache-2.0).
- **FlowApps branding, logo and symbol:** Reach Neo (trademark of Reach Neo).

Slideflow is not affiliated with or endorsed by ArtCraft or the DeckCraft contributors.

## License

Slideflow is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE), at your option.

**Copyright (c) 2026 Reach Neo and the Slideflow contributors.**
