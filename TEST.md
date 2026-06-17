# Shomer Beach — Test & Verification

App pressure-tested in a real headless Chromium preview (mobile viewport 375×812,
He + En). **Zero console errors or warnings** across the entire session.

## How it was built (brand parity guarantee)

Shomer Beach must share the **exact** Shomergency brand/layout/engine. To guarantee
that, the build is a **3-way merge**, not a hand-port:

- **base** = the Shomergency `shomer.html` commit Shomer Beach was originally forked from
- **theirs** = the latest Shomergency `shomer.html` (which had gained a full SOS
  *safety state machine* — cancel-countdown, hold-to-arm, rate-limit, trust,
  Real/Accidental/Test resolution — after the fork)
- **mine** = the existing coastal content re-skin

Merging *theirs* (engine) into *mine* (content) re-applied **every** brand/engine
improvement while keeping the coastal content. Result: identical brand + engine to
the latest Shomergency, coastal content only. One conflict (in `activateSOS`) was
resolved in favour of the new engine, re-branded `שומר → שומר חוף`.

## Flows verified ✅

| Area | Result |
|------|--------|
| Onboarding (account → geo skip → alarm → finish) | ✅ branding "שומר חוף / Citizens For the Coast"; finish button fixed to single `✓ כניסה לשומר חוף` |
| Main app shell | ✅ header `שומר חוף™` + gold lifebuoy logo, real Leaflet coast map, coastal data banner (רט"ג · משרד להגנת הסביבה · עונת מדוזות) |
| **SOS — countdown** | ✅ tap → alarm + cancel-countdown overlay (conic ring, big number, cancel button) |
| **SOS — cancel = no trace** | ✅ cancel in-window → phase idle, **history stays empty, no map pin, strip off**, private false-alarm counter +1 |
| **SOS — activate** | ✅ countdown expiry → active, history logged, strip "🚨 SOS פעיל — אזעקה פועלת · מיקומך שותף" |
| **SOS — resolve** | ✅ resolve prompt (Real/Accidental/Test); `accidental` scrubs pin/card + increments trust |
| SOS auto-dial | ✅ adapted to coastal: confirms **101 / מד״א** (was police 100) — matches the emergency-tab guidance |
| Report sheet | ✅ "סוג המפגע" + 6 coastal hazard types with icons 🌊🦈🐬🐢🗑️🛢️ |
| Emergency tab | ✅ 101 מד"א · 100 משטרה/שיטור ימי · 102 כבאות · מציל בחוף · *3639 רט"ג `לאימות` · *6911 משרד להגנת הסביבה `לאימות` |
| Updates feed | ✅ coastal incidents (rip current, jellyfish swarm, sea-turtle rescue, oil sheen, hazardous waste) |
| Detail panel | ✅ opens with real lat/lng coords (e.g. חוף גורדון, תל אביב) |
| Map legend | ✅ coastal categories (SOS חי · זרמים/טביעה · מדוזות/כריש · זיהום/פסולת · דליפת נפט · חי ים במצוקה · חי ים פצוע/מת) |
| **English localization** | ✅ report options, emergency intro, legend, data banner, `verify` tags all switch to English (a Shomergency report-option localization gap that the coastal build fixes) |
| Responsive / mobile | ✅ verified at 375×812 |

## Security / quality

- `Content-Security-Policy` meta present (identical to Shomergency).
- **No `eval`** anywhere. User-supplied data rendered via `textContent` / `ESC()`;
  `innerHTML` used only for trusted static templates.
- Accessibility: `role`/`aria-*` on SOS overlays, radios, switches; skip-link;
  `aria-pressed` on the SOS button; high-contrast media query.
- Service worker: network-first navigation + foreign-cache purge on the shared
  `*.github.io` origin; cache bumped to `v2` for this release.

## Not covered by automated checks

- Real multi-device broadcast / rate-limit / trust enforcement (by design — see
  README "What's real vs. what needs a backend").
- Native auto-dial (browser opens the dialer; a native wrapper would place the call).
- Real push delivery (uses local notifications in-app).
