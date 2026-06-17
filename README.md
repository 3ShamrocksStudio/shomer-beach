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
- **Instant SOS** with an anti-abuse safety state machine:
  - the alarm fires **immediately** on your own phone, then a **cancel countdown**
    (5/7/10s) runs *before* anything is broadcast — cancel in time and it leaves
    **no trace** (no map pin, no feed card, no broadcast);
  - optional **hold-to-arm** (2s press) to prevent pocket-dials;
  - a per-day **rate limit** and a **trust/reputation** readout;
  - on resolution you mark it **Real / Accidental / Test** — accidental & test are
    scrubbed from the map and never shown to others.
  - Plus live location share, **shake-to-SOS**, and a **Dead Man's Switch**
    (great before swimming/diving alone).
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

## What's real vs. what needs a backend

This is a **front-end prototype / PWA**. Everything works end-to-end *on the
device*, but anything that implies other people must be enforced by a server in a
real deployment. Being honest about the line:

**Real today (works for one device, offline-capable):**
- Onboarding, profile, language (He/En), full PWA install + offline shell.
- Real geolocation, live Leaflet/OSM map, collapsible legend.
- Report flow with photo capture and `localStorage` persistence.
- SOS alarm (real Web Audio), shake-to-SOS, Dead Man's Switch, lock-screen push
  (local), cancel-countdown "no-trace" logic, resolution scrubbing.
- One-tap dialing of real emergency numbers (`tel:` links).

**Simulated locally — needs a backend to be real:**
- **Broadcast / fan-out** of an SOS to nearby guardians (shown as a simulation).
- The **per-day rate limit** and **trust/reputation** score — client-side only and
  trivially bypassable (clear storage); a real system MUST enforce these
  server-side, keyed to the account/device.
- "Guardians responding" counts and the **demo feed/map incidents** are seeded
  sample data, not live reports from real users.
- The beach **statistical overview** markers are aggregate references, not a live feed.

**Authority numbers tagged `לאימות / verify`** (*3639 NPA, *6911 Min. of
Environmental Protection) must be confirmed with the official body before launch.

---

© 2026 **3Shamrocks Studio** · Shomer Beach™ · All rights reserved.
