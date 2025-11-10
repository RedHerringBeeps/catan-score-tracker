# Catan Score Tracker — Design Notes (Master Version)

_Last updated: 2025‑11‑10_

## 1) Entities & Counters
### Core
- Settlements (int ≥ 0): +1 each; Cities↑ consumes Settlements; Cities↓ refunds Settlements.
- Cities (int ≥ 0): +2 each; bidirectional with Settlements.
- Victory Cards (int ≥ 0): +1 each.

### Seafarers
- Islands (int ≥ 0): +2 each (only when Seafarers is enabled).

### Traders & Barbarians
- Gold (int ≥ 0): unique max +1; unique min −2; ties at max +0; ties at min −2 for minima.
- Harbors (int ≥ 0): drives Harbormaster (derived).

### Cities & Knights
- Metropolises (Science/Trade/Politics): booleans, globally exclusive, +2 each.
- Merchant: boolean, globally exclusive, +1.

## 2) Derived Awards
### Longest Road (base)
- Source: Roads (int ≥ 0).
- Threshold: roads ≥ 5 (raw counter).
- Ownership: unique top wins; tie keeps **incumbent** if still among top; otherwise none.
- Points: +2.

### Harbormaster (T&B)
- Source: Harbors (int ≥ 0).
- Threshold: harbors ≥ 3.
- Ownership: unique top wins; tie keeps **incumbent**.
- Points: +2.

## 3) Scoring
```
score =
  togglesSum                        // metros (+2 each) + merchant (+1), gated by expansions
  + (hasLongest ? 2 : 0)
  + ((T&B && hasHarborMaster) ? 2 : 0)
  + vpCards
  + (Seafarers ? islands*2 : 0)
  + settlements
  + cities*2
  + (T&B ? goldRankBonus : 0)
```

## 4) State & Persistence
- Players: array; numeric fields coerced to int ≥ 0.
- Expansions: { ck, seafarers, tb }.
- localStorage: `catan.players.v3`, `catan.expansions.v2`.
- Reset Scores (keeps names), Reset All, Clear Save.

## 5) Interaction
- Large ± buttons with press‑and‑hold (initial 300ms, repeat 120ms). Single taps ±1.
- City↔Settlement conversion with guards.
- Exclusivity: metropolises & merchant are global exclusive; LR/HB are derived read‑only.

## 6) Rendering
- LR/HB computed synchronously (`useMemo + useRef`) for zero‑lag points.
- Award flags included in memo deps for tile totals.

## 7) UI Decisions
- Catan‑themed palette, wood texture background, gradient borders (layered bg).
- Static leader highlight (no breathing).
- Award badges with thicker border, ring, and shadow.
- Deluxe only; fullscreen toggles whole document.
- “Total Cities: N” compact chip above tiles.

## 8) Changelog (2025‑11‑10)
- Longest Road: counter‑based, ≥5, incumbent advantage, sync compute, integer coercion, memo deps fixed.
- Harbormaster: ≥3, incumbent advantage, sync, memo deps fixed.
- Gold bonus: +1 unique max, −2 unique min.
- Stability: removed stray fragments; corrected compute ordering.
