# Project Brief

## Idea
PUBG Taego map safety pin website.

## Problem
When playing PUBG, it is hard to quickly know which nearby positions are relatively safe.

## User Need
The user wants to look at a Taego map during gameplay and quickly decide where to move next by checking nearby safe-position pins.

## MVP
A static web page that shows a high-resolution Taego map with fixed safe-position pins.

## MVP Scope
- Show one high-resolution Taego map image.
- Show fixed pins for safe positions.
- Use hardcoded pin coordinates for now.
- Support mouse wheel zoom.
- Support drag to pan.
- Keep panning inside the map bounds.
- Zoom around the mouse cursor position.
- Keep pins small while zooming.
- Target desktop first.

## Out of Scope
- Pin click interactions.
- Position descriptions.
- Safety scores.
- Current player location input.
- Route recommendation.
- Login or data storage.
- Admin/editor features.
- Mobile optimization beyond basic display.

## First Version
- One `index.html`.
- One `styles.css`.
- One high-resolution Taego map image.
- About 10 temporary safe-position pins.

## Current Implementation
- `index.html`: static page, map, temporary pins, zoom/pan script.
- `styles.css`: map layout and pin styling.
- `assets/taego-map-high.jpg`: 4096x4096 Taego map generated from PUBG official `api-assets`.
- `assets/taego-map.webp`: older 1008x1008 map kept for reference.

## Important Product Decision
Pins should not be selected only by looking at the 2D map image.

PUBG safety depends on real in-game terrain, height, cover, sightlines, vehicle routes, circle state, and enemy positions. For the MVP, pins should represent relatively safe non-building terrain positions, but candidates should come from community guides, YouTube gameplay, or direct playtesting.

## Pin Criteria
- Prefer non-building terrain positions.
- Prefer ridges, reverse slopes, rocks, tree cover, and terrain with exit routes.
- Avoid cities, building interiors, roads, bridges, and open fields.
- Treat pins as "generally useful terrain positions", not always-safe answers.

## Future Direction
- Let users submit good position pins.
- Add voting or likes.
- Promote commonly validated pins.
- Add filters later, such as solo/squad, early/mid/late game, ridge/building/vehicle, or circle context.
