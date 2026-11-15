# Lychee Juicebox

**An Earth map becomes a sound you can explore.** Lychee Juicebox is Team Lychee's 2026 NASA Space Apps project. Visitors choose a supplied or uploaded map, select an area, and hear a scan of its rendered colors. The project treats the image as an artistic input; it does not convert the map back into measured geophysical values.

This is a **parent repository**. It pins two independent Git repositories as submodules. The applications stay in the original repositories, and any existing deployment connections remain unchanged.

| Submodule | Contains | Pinned revision |
| --- | --- | --- |
| [`web-and-map-api/`](https://github.com/Mretmna/team-lychee-nasaspaceapps-27) | Next.js frontend, FastAPI map service, bundled media, offline video preparation | [`1ff8811`](https://github.com/Mretmna/team-lychee-nasaspaceapps-27/commit/1ff881180fffbbdafad90fb4bf5aa16ded97bec3) |
| [`sound-api/`](https://github.com/Mretmna/team-lychee-nasaspaceapps-backend-27) | FastAPI image analysis and STRAUSS audio renderer | [`d6c06d3`](https://github.com/Mretmna/team-lychee-nasaspaceapps-backend-27/commit/d6c06d3c3e5ed13066e3f48e0385e9050cd46863) |

## At a glance

| Step | Component | What happens |
| --- | --- | --- |
| 1. Choose | Next.js frontend | Select a map or video frame and an area to hear. |
| 2. Prepare | Browser and map API | Crop the image; validate uploads or resolve a city when needed. |
| 3. Sonify | FastAPI sound API + STRAUSS | Analyze image colors and render a WAV with a color timeline. |
| 4. Explore | Next.js frontend | Play the sound, follow the scan marker, or use DJ and Tone.js modes. |

1. The browser reads a built-in Earth image, an animation frame, or a user-supplied global map.
2. It selects a circle, square, or the entire map using latitude, longitude, and radius.
3. The map API validates prepared uploads and can resolve cities or store maps. Built-in map crops are prepared in the browser.
4. The sound API scans the selected image into 48 positions × 12 bands, maps color and brightness to four synthesized voices, and returns a complete WAV file.
5. The frontend plays that WAV while moving the visible scan marker. Optional DJ mode scrubs short audible samples; optional Tone.js playback resynthesizes notes from the WAV in the browser.

**Animated-map detail:** the current sound is generated from the **first selected video frame**. The video moves in sync with playback, but its full frame-feature timeline does not currently drive the active sound renderer. See [Architecture](docs/ARCHITECTURE.md#animated-map-behavior).

## Documentation

| Guide | What it covers |
| --- | --- |
| [Architecture](docs/ARCHITECTURE.md) | Components, request sequence, state, persistence, runtime boundaries |
| [Maps and data](docs/MAPS_AND_DATA.md) | Map sources, geographic selection, upload rules, video feature pipeline, provenance |
| [Sonification](docs/SONIFICATION.md) | Image sampling, color-to-sound mapping, templates, spatial audio, DJ and instrument modes |
| [API and operations](docs/API_AND_OPERATIONS.md) | Endpoint contracts, environment variables, local development, verification, deployment boundaries |

The source repositories retain their own focused documentation: [web/map README](https://github.com/Mretmna/team-lychee-nasaspaceapps-27/blob/1ff881180fffbbdafad90fb4bf5aa16ded97bec3/README.md), [ocean data methodology](https://github.com/Mretmna/team-lychee-nasaspaceapps-27/blob/1ff881180fffbbdafad90fb4bf5aa16ded97bec3/backend/docs/data-methodology.md), and [sound API README](https://github.com/Mretmna/team-lychee-nasaspaceapps-backend-27/blob/d6c06d3c3e5ed13066e3f48e0385e9050cd46863/backend/README.md). This parent guide describes the **pinned code** and resolves historical differences between those documents and the current UI.

## Clone and run

```sh
git clone --recurse-submodules https://github.com/Mretmna/lychee-juicebox.git
cd lychee-juicebox
```

If the parent is already cloned, run `git submodule update --init --recursive`. Start the map API on port 8000, the sound API on port 8001, and Next.js on port 3000 using the commands in [API and operations](docs/API_AND_OPERATIONS.md#local-development). The homepage is `/`; the visitor tutorial is `/tutorial`; FastAPI's interactive references are available at `/docs` on each local API port.

## Repository rule

Make code changes and commits **inside the relevant child repository**. Commit the updated submodule pointer in this parent only when you want it to reference that child revision. This parent contains documentation and Git references; it has no build or deployment pipeline. No Vercel, Cloud Run, domain, or DNS settings are changed here.
