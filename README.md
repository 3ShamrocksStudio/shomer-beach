# Shomer Beach · שומר חוף

**Citizens For the Coast** — the coastal & marine vertical of the **Shomer** safety platform.

Shomer Beach shares the **exact same brand, layout and design system** as
[Shomergency](https://3shamrocksstudio.github.io/shomergency/) and
[Shomer Forest](https://3shamrocksstudio.github.io/shomer-forest/) — the only
differences are the **content & purpose**: location focus (Israel's beaches and
sea), the **hazard/event types**, and the relevant **authorities**.

## What it does

- **Live coastal-hazard map** — neutral grayscale basemap with clear, colour-coded
  markers and a compact collapsible legend.
- **Report a beach hazard** with photo + real geolocation:
  - 🌊 Dangerous currents / drowning hazard
  - 🦈 Jellyfish / shark sighting (dangerous animal)
  - 🐬 Marine animal in distress (stranded / entangled)
  - 🐢 Injured / dead marine animal
  - 🗑️ Hazardous trash / pollution
  - 🛢️ Oil / chemical spill
- **Instant SOS** — loud multi-tone alarm engine, live location share, shake-to-SOS,
  and a Dead Man's Switch (great before swimming/diving alone).
- **Coastal authorities** — 101 MDA, 100 Police / Marine Police, 102 Fire & Rescue,
  lifeguard guidance, Israel Nature & Parks Authority and the Ministry of
  Environmental Protection. *Numbers tagged "verify / לאימות" must be confirmed
  with the official body before relying on them.*
- Hebrew + English, RTL/LTR, PWA installable, offline-capable.

## Tech

Single self-contained `shomer-beach.html` (sanitized DOM, no `eval`, strict CSP).
Leaflet + OpenStreetMap tiles at runtime. `localStorage` persistence. PWA via
`manifest.json` + a **network-first** service worker that purges foreign caches on
the shared `*.github.io` origin.

The map's beach markers are an **aggregate statistical overview**, not specific
incidents. Personal pins come only from user reports and live SOS.

---

© 2026 **3Shamrocks Studio** · Shomer Beach™ · All rights reserved.
