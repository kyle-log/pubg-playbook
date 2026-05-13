# Next Steps

## Current Status
The MVP shell is working.

- High-resolution Taego map is displayed.
- Mouse wheel zoom works.
- Zoom uses the mouse cursor as the center.
- Drag pan works.
- Pan is bounded inside the map.
- Pins stay small while zooming.
- Current pins are temporary placeholders.

## Main Remaining Task
Replace temporary pins with real safe terrain position pins.

## Important Constraint
Do not choose safety pins by only looking at the map image.

Taego safety positions must be researched from:
- PUBG community posts.
- YouTube guides or gameplay.
- Competitive/ranked rotation discussions.
- Direct playtesting.

## Research Goal
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

## Suggested Workflow
1. Research Taego safe terrain/rotation positions from community and YouTube.
2. Record each candidate with source link and short reason.
3. Add only evidence-backed candidates to the map.
4. Open the local page and adjust coordinates visually.
5. Playtest and refine.

## Useful Search Queries
- `PUBG Taego rotation guide ridges`
- `PUBG Taego safe positions`
- `PUBG Taego ranked rotation`
- `PUBG Taego terrain guide`
- `배그 태이고 운영 위치`
- `배그 태이고 능선 자리`
- `배그 태이고 안전한 자리`
- `배그 태이고 자기장 운영`

## Next Implementation Improvement
Before adding many real pins, move pin data out of HTML into a separate data structure or JSON-like array. This will make future user-submitted pins easier to support.

## Map Label Idea
Add optional area alias labels to the map.

Each Taego region can have player-used nicknames or callouts. The map should make those aliases easy to check during gameplay, ideally as a toggleable overlay so the labels do not clutter the pin view.

Useful details to track:
- Official area name.
- Korean player nickname or callout.
- Optional short note explaining what the nickname refers to.
- Label position on the map.
