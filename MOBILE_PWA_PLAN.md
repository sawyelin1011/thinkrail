---
id: plan-mobile-pwa
type: plan
status: draft
title: Mobile browser access on same network + responsive PWA-ready plan
parent: architecture
---

# Mobile browser access on same network + responsive PWA-ready plan

## Goal

Make ThinkRail usable from a mobile browser on the same LAN as the host, with a responsive
mobile shell and PWA installability/offline shell, without rewriting panels or store.

## Scope

- Host binding: allow `--host 0.0.0.0` (or LAN IP) so mobile devices on the same network can reach the web UI.
- Responsive shell: single-view mobile layout riding on the existing responsive composition split.
- PWA: manifest, service worker, installable, offline shell.
- Touch-friendly: gestures, viewport, safe areas.

## Non-goals

- Native mobile app.
- Cross-network/remote access (tunneling) — out of scope; same network only.

## Milestones

1. Host/network access
   - CLI `--host` default localhost; document LAN usage; CORS/origin handling for mobile origin.
   - Auth: pairing/token for LAN clients.
2. Responsive mobile shell
   - Breakpoints; single-view navigation; collapsible panels.
3. PWA packaging
   - manifest.json, icons, service worker caching shell; offline fallback.
4. Touch & ergonomics
   - tap targets, swipe, safe-area insets, virtual keyboard handling.
5. Testing
   - Playwright mobile viewport e2e; Lighthouse PWA audit.

## Acceptance criteria

- Opening host URL from phone on same Wi-Fi loads UI and connects over WS.
- Install prompt appears; app installs to home screen.
- Offline load shows cached shell.
- No desktop-only feature breaks on mobile viewport.

## Risks

- Security of exposing host on LAN; mitigate with token + pairing.
- Service worker caching stale assets; versioned cache.

## References

- apps/web/SPEC.md (responsive shell, PWA note)
- apps/cli/SPEC.md (--host)
