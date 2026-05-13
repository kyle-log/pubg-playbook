# PUBG Playbook

## AI Rules

### Response Style
- Always answer in Korean unless the user explicitly requests another language.
- Keep answers short, concise, and easy to scan.
- Start with the conclusion or next action.
- Avoid long explanations unless the user asks for detail.
- Prefer bullets over long paragraphs.
- When planning, show only the immediate next steps.

### Collaboration
- Clarify vague ideas before implementation.
- Ask only necessary questions.
- Make practical assumptions when the risk is low, and state them briefly.

## Project Brief

### Idea
PUBG Taego map safety pin website.

### Problem
When playing PUBG, it is hard to quickly know which nearby positions are relatively safe.

### User Need
The user wants to look at a Taego map during gameplay and quickly decide where to move next by checking nearby safe-position pins.

### MVP
A static web page that shows a high-resolution Taego map with fixed safe-position pins.

### MVP Scope
- Show one high-resolution Taego map image.
- Show fixed pins for safe positions.
- Use hardcoded pin coordinates for now.
- Support mouse wheel zoom.
- Support drag to pan.
- Keep panning inside the map bounds.
- Zoom around the mouse cursor position.
- Keep pins small while zooming.
- Target desktop first.

### Out of Scope
- Pin click interactions.
- Position descriptions.
- Safety scores.
- Current player location input.
- Route recommendation.
- Login or data storage.
- Admin/editor features.
- Mobile optimization beyond basic display.

### First Version
- One `index.html`.
- One `styles.css`.
- One high-resolution Taego map image.
- About 10 temporary safe-position pins.

### Current Implementation
- `index.html`: static page, map, temporary pins, zoom/pan script.
- `styles.css`: map layout and pin styling.
- `assets/taego-map-high.jpg`: 4096x4096 Taego map generated from PUBG official `api-assets`.
- `assets/taego-map.webp`: older 1008x1008 map kept for reference.
- Plane route and safe circle drawing are supported from separate map controls.

### Deployment
- GitHub Pages: https://kyle-log.github.io/pubg-playbook/

## Product Decisions

Pins should not be selected only by looking at the 2D map image.

PUBG safety depends on real in-game terrain, height, cover, sightlines, vehicle routes, circle state, and enemy positions. For the MVP, pins should represent relatively safe non-building terrain positions, but candidates should come from community guides, YouTube gameplay, or direct playtesting.

### Pin Criteria
- Prefer non-building terrain positions.
- Prefer ridges, reverse slopes, rocks, tree cover, and terrain with exit routes.
- Avoid cities, building interiors, roads, bridges, and open fields.
- Treat pins as "generally useful terrain positions", not always-safe answers.

## Current Status

The MVP shell is working.

- High-resolution Taego map is displayed.
- Mouse wheel zoom works.
- Zoom uses the mouse cursor as the center.
- Drag pan works.
- Pan is bounded inside the map.
- Pins stay small while zooming.
- Plane route drawing works by selecting a start and end point.
- Safe circle drawing uses 8x8km map scale and phase-specific PUBG white-circle diameters.
- Current pins are temporary placeholders.

## Circle Scale

Taego is treated as an 8x8km map, so the map width equals 8000m.

Circle diameter on the UI is calculated as:

`circle diameter percent = phase diameter meters / 8000 * 100`

Current phase diameter data:

| Phase | Diameter |
| --- | ---: |
| 1 | 3994.1m |
| 2 | 2396.5m |
| 3 | 1318.1m |
| 4 | 724.9m |
| 5 | 362.5m |
| 6 | 181.2m |
| 7 | 90.6m |
| 8 | 45.3m |

## Main Remaining Task

Replace temporary pins with real safe terrain position pins.

## Research Workflow

Do not choose safety pins by only looking at the map image.

Taego safety positions must be researched from:
- PUBG community posts.
- YouTube guides or gameplay.
- Competitive/ranked rotation discussions.
- Direct playtesting.

### Research Goal
Find non-building terrain positions that are commonly useful.

Good candidates:
- Ridges.
- Reverse slopes.
- Rocks or tree cover.
- Hill edges.
- Positions near escape routes.
- Positions that avoid obvious road/open-field exposure.

Avoid:
- Buildings and compounds.
- City centers.
- Main roads.
- Bridges.
- Wide open fields.
- Positions with no exit route.

### Suggested Workflow
1. Research Taego safe terrain/rotation positions from community and YouTube.
2. Record each candidate with source link and short reason.
3. Add only evidence-backed candidates to the map.
4. Open the local page and adjust coordinates visually.
5. Playtest and refine.

### Useful Search Queries
- `PUBG Taego rotation guide ridges`
- `PUBG Taego safe positions`
- `PUBG Taego ranked rotation`
- `PUBG Taego terrain guide`
- `배그 태이고 운영 위치`
- `배그 태이고 능선 자리`
- `배그 태이고 안전한 자리`
- `배그 태이고 자기장 운영`

## Next Implementation Improvements

- Move pin data out of HTML into a separate data structure or JSON-like array before adding many real pins.
- Add optional area alias labels as a toggleable overlay so labels do not clutter the pin view.

Useful label details to track:
- Official area name.
- Korean player nickname or callout.
- Optional short note explaining what the nickname refers to.
- Label position on the map.

## Future Direction

- Let users submit good position pins.
- Add voting or likes.
- Promote commonly validated pins.
- Add filters later, such as solo/squad, early/mid/late game, ridge/building/vehicle, or circle context.

## Pin Research

### Status
Research in progress. Do not treat these as final safe pins yet.

### Source Notes

#### PUBGZone Taego guide
- URL: https://pubgzone.com/pubg-taego-map/
- Notes:
  - Taego punishes late open-field rotations.
  - Early rotation, ridge control, reverse slopes, and covered movement are repeatedly emphasized.
  - Buk San Sa has high-ground value, but staying too long without a rotation plan can get teams boxed in.
  - Terminal is high traffic and reset-heavy, so it should not be treated as a default safe terrain pin.
- Pin impact:
  - Prefer terrain near ridges, reverse slopes, and covered exits.
  - Avoid open paddies, late road crossings, and high-traffic POI interiors.

#### Official PUBG Taego map page
- URL: https://www.pubg.com/ko/game-info/maps/taego
- Notes:
  - Taego is an 8x8 map.
  - Official map copy describes varied terrain from reed fields to Ho San Prison.
  - Officially highlighted landmarks include Terminal, Buk San Sa, Ho San Prison, and School.
- Pin impact:
  - Terrain variety matters, so pins should describe the exact cover type instead of only naming a nearby POI.
  - Named landmarks should be treated as navigation references, not automatically safe locations.

#### CompetitivePUBG discussion: Taego terrain issues
- URL: https://www.reddit.com/r/CompetitivePUBG/comments/12z26ke
- Notes:
  - Multiple players describe Taego as having many flat/open areas with limited playable terrain.
  - One detailed comment calls out Army Base / north of Yong Cheon as comparatively playable.
  - Bridge and island shifts are repeatedly described as major rotation risks.
- Pin impact:
  - Candidate pins near Army Base and north of Yong Cheon deserve closer review.
  - Avoid bridge-dependent pins and exposed open fields.

### Candidate Regions To Verify

#### Army Base / north of Yong Cheon terrain
- Confidence: medium
- Reason: Mentioned in competitive discussion as one of the more playable open-terrain areas.
- Needs:
  - Visual coordinate adjustment on the local map.
  - Gameplay/video confirmation of exact ridge, dip, rock, or tree-cover position.

#### Buk San Sa surrounding high ground
- Confidence: low-medium
- Reason: Guide notes high-ground value, but also warns about surrounding risk and getting boxed in.
- Needs:
  - Identify specific edge positions with exits.
  - Avoid committing to the central landmark or obvious compounds.

### Avoid For Now

#### Terminal
- Reason: High traffic and third-party pressure.
- Decision: Do not add as a "safe" MVP pin unless a specific terrain edge is later verified.

#### Bridges and bridge approaches
- Reason: Community discussion repeatedly flags bridge shifts as major choke risks.
- Decision: Avoid default safe pins near bridge-dependent routes.

#### Open fields and paddies
- Reason: Multiple sources emphasize that exposed movement is heavily punished.
- Decision: Avoid unless the exact spot has hard cover, terrain dip, or a clean exit.
