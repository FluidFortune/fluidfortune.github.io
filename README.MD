# fluidfortune.com

The public website for **Fluid Fortune** — an independent software forge building sovereign computing tools.

**Live site:** [fluidfortune.com](https://fluidfortune.com)

---

## What this repo is

This is the source for the Fluid Fortune public website. It is a static site — no build step, no framework, no server-side rendering. Every page is a self-contained HTML file. Deploy with `git push`. That's it.

The site documents the Fluid Fortune forge, its projects, and its published architectural work. The primary subject is **Pisces Moon OS** — a sovereign computing platform for the ESP32-S3 and ESP32-P4 hardware class.

---

## Structure

```
/                           — Main site
├── index.html              — Homepage (forge overview, projects, media)
├── pisces-moon.html        — Pisces Moon OS platform page (tabbed)
├── sovereignty.html        — Sovereignty white paper (tabbed app panel)
├── spi-bus-treaty.html     — SPI Bus Treaty architectural whitepaper
├── device-architecture.html — T-Deck Plus / T-LoRa Pager / Cardputer ADV comparison
├── project.html            — The Fluid Fortune Project (living document)
├── engineering-record.html — Engineering record
├── consulting.html         — Consulting services
├── rates.html              — Rate card
├── audits.html             — Security audits
├── process.html            — Process documentation
├── case-studies.html       — Case studies
├── writing.html            — Writing and media
├── contact.html            — Contact
├── sitemap.xml             — Sitemap (submitted to Google Search Console)
├── robots.txt              — Crawler directives
├── llms.txt                — AI crawler standard (llmstxt.org)
├── style.css               — Main stylesheet
└── *.jpeg / *.jpg          — Images
```

The portfolio lives at `portfolio/`. Individual project pages are standalone HTML files.

---

## The primary project: Pisces Moon OS

Pisces Moon OS is a general-purpose sovereign computing platform for the ESP32-S3 and ESP32-P4 hardware class.

**Firmware repo:** [github.com/FluidFortune/pisces-moon-os](https://github.com/FluidFortune/pisces-moon-os)
**Linux/Android repo:** [github.com/FluidFortune/pisces-moon-linux](https://github.com/FluidFortune/pisces-moon-linux)
**Live demo:** [piscesdemo.fluidfortune.com](https://piscesdemo.fluidfortune.com)
**Lety IDE:** [lety.fluidfortune.com](https://lety.fluidfortune.com)

### Two inventions that did not exist before this project

**The Ghost Engine** — a persistent Core 0 process that wardrives, scans BLE, and logs GPS continuously, always, regardless of what the operator is doing on Core 1. The device is always collecting. The operator never has to think about it.

**The SPI Bus Treaty** — the first named architectural standard for shared-bus arbitration on the ESP32-S3. A formal behavioral protocol governing all components that share the SPI bus. The reason the Ghost Engine can run unconditionally. Without it, Core 0 and Core 1 destroy each other over the shared bus. With it, the device is always collecting.

### Hardware targets

| Target | Device | Tier | Status |
|--------|--------|------|--------|
| 1A | LilyGO T-Deck Plus (ESP32-S3) | Native firmware | Production — 49 apps |
| 1B | LilyGO T-LoRa Pager (ESP32-S3) | Native firmware | Production — 52 apps |
| 2 | Pisces Moon Linux (x86/ARM) | HTML/JS suite | Live — 77 apps |
| 3 | Android APK | HTML/JS suite | Live |
| 4 | Luckfox Pico 86 Panel (RV1106) | HTML/JS suite | Live |
| 5 | M5Stack Cardputer ADV (ESP32-S3) | Native firmware | Alpha — 47 apps, Cap LoRa868 module pending |
| 6 | ESP32-P4 / Elecrow CrowPanel 7" | Native firmware | Alpha — first boot May 13, 2026 |

### Ten novel engineering problems — all documented

1. **SPI Bus Conflict** → The SPI Bus Treaty
2. **Memory Exhaustion** → PSRAM heap redirection
3. **Dual-Core Task Synchronization** → FreeRTOS mutex + sentinel flags
4. **Dense RF Environment Instability** → Stack sizing, buffer limits, drain loops
5. **Security Architecture Under Hardware Timing Constraints** → Metadata-only Nuke
6. **GPS Module Hardware Variation** → Baud rate auto-detection
7. **GPIO Pin Collision** (T-LoRa Pager SD_CS = T-Deck TOUCH_RST on GPIO 21) → Conditional compilation
8. **SPI Bus State Corruption** → Deferred SD mount with cold SPI restart
9. **Ghost Engine Silent Failure** → Lazy session-file creation
10. **ELF Execution Without Hardware Isolation** → Three-layer PMS sandbox (first documented on ESP32-S3)

### What makes the Cardputer architecturally distinct

The Cardputer ADV is the third Tier 1 device and the most architecturally different from T-Deck and T-LoRa Pager:

- **Two separate SPI buses** — display on HSPI (no Treaty contention), SD + LoRa on FSPI (Treaty governs this bus). Display updates at full speed during wardrive scans.
- **M5Cardputer library for keyboard** — TCA8418 controller, but the M5Cardputer library handles all matrix scanning and Fn-layer resolution. Pisces Moon wraps it into universal `PM_KEY_*` constants.
- **240×135 — 32,400 pixels** — roughly 40% of the T-Deck Plus. Every app UI needed rethinking: textSize=1 throughout, 14px header bars, ring-buffer BIOS auto-scroll, Cardputer-specific splash geometry.
- **Cap LoRa868 module** — SX1262 LoRa + AT6668 GNSS (GPS/Beidou/GLONASS/Galileo/QZSS) over the 2×7-pin expansion header. Without it, wardrive runs WiFi + BLE only.
- **47 apps** — same seven categories as T-Deck and T-LoRa Pager. Snake fully reflowed for 240×135 in v1.2.0. Pac-Man, Galaga, SimCity stubbed pending geometry work.

Cardputer-specific build: `pio run -e cardputer_adv`. Uses `partitions_cardputer.csv` (8 MB) — do not flash with the T-Deck/Pager 16 MB partition table.

### Architectural documentation

| Page | Content |
|------|---------|
| [sovereignty.html](https://fluidfortune.com/sovereignty.html) | Full technical and philosophical white paper. DEF CON 34 CFP #1349. |
| [spi-bus-treaty.html](https://fluidfortune.com/spi-bus-treaty.html) | SPI Bus Treaty architectural whitepaper. Four field failures. Design primitives. |
| [device-architecture.html](https://fluidfortune.com/device-architecture.html) | T-Deck Plus vs T-LoRa Pager vs Cardputer ADV hardware comparison. |

---

## Philosophy

**Sovereignty by design, not retrofit.** Every architectural decision starts from: does the operator control this, or does a vendor?

**The methodology:** Name the constraint. Document the protocol. Make it a platform contract.

**The receipt is $144.** T-Deck Plus hardware + cloud AI. Six weeks. One person. Ten novel engineering problems solved. Six deployment targets confirmed.

---

## The forge

Fluid Fortune is an independent forge founded by **Eric Becker** — The Court Jester of Vibe Coding.

| | |
|---|---|
| Contact | [forge@fluidfortune.com](mailto:forge@fluidfortune.com) |
| Blog | [blog.fluidfortune.com](https://blog.fluidfortune.com) |
| Podcast | [podcast.fluidfortune.com](https://podcast.fluidfortune.com) |
| Portfolio | [portfolio.fluidfortune.com](https://portfolio.fluidfortune.com) |

---

## Projects

**Core forge:**
- [Pisces Moon OS](https://fluidfortune.com/pisces-moon.html) — Sovereign computing platform
- [Spadra Smelter](https://spadra-smelter.fluidfortune.com) — RF intelligence analysis
- [The Phantom](https://github.com/FluidFortune/The-Phantom) — Local AI, no API keys
- [Trojan Horse](https://github.com/FluidFortune/trojan-horse) — Native app wrapper, no Electron
- [The Lighthouse](https://github.com/FluidFortune/the-lighthouse) — Session bridge
- [WozBot](https://wozbot.fluidfortune.com) — Local AI proof-of-concept
- [Punky](https://punky.fluidfortune.com) — GitHub-native blog editor
- [Little Soul](https://little-soul.fluidfortune.com) — GitHub-native website builder

**Side projects:**
- [Vibe Calc](https://vibecalc.fluidfortune.com)
- [The DeNiro Zone](https://the-deniro-zone.fluidfortune.com)
- [Amara](https://amara.fluidfortune.com)
- [Portland](https://portland.fluidfortune.com)
- [True Crime](https://truecrime.fluidfortune.com)

---

## License

Website content and code © 2026 Eric Becker / Fluid Fortune, unless otherwise noted in the license.

See [LICENSE](LICENSE) for full terms.

Pisces Moon OS firmware: [AGPL-3.0-or-later](https://www.gnu.org/licenses/agpl-3.0.html)
Pisces Moon application layer: MIT

---

*The Ghost Engine never stops. The SPI Bus Treaty is why.*
