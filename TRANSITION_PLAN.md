# Auto-generated stage transitions — feature plan (parked)

Status: **parked** (2026-07-09). Idea captured for later; not started.

## Goal

Let the user upload only the stage stills (Stage 1, Stage 2, Stage 3) and have
the editor **auto-generate a short transition** that morphs one stage into the
next, played during the level-up. "Only add images."

Original ask: generate a greenscreen video using the previous stage and the next
stage as start/end frames → trim to ~1s (optional length) → choose FPS → remove
the greenscreen → use the result as the transition.

## Crucial constraint

The API call must happen at **design time in the editor**, never inside the
exported ad. Exported playables run in a sandbox (Facebook/Google/Unity/
Mintegral) with no external calls, a tight size budget, and instant load — you
cannot call a video-gen API from a shipped ad (key would leak, too slow, networks
reject it).

Model: upload stills → click **Generate transition** in the editor → editor calls
the API, keys out the green, bakes the finished frames into the asset → the
**export contains only the pre-rendered transition**. The API key lives in a local
field (localStorage, like the project list) and never touches the export.

## Pipeline

1. Compose keyframes — put the stage PNGs on a green background (start + end frame).
2. Call the video API with those as first/last frame → generated morph clip.
3. Trim + resample to chosen length (default 1s) and FPS — client-side via WebCodecs.
4. Chroma-key the green out of each frame → transparency.
5. Bake keyed frames into a transition asset (frame sequence / sprite sheet).
6. Runtime (`buildAd`): on the triggering tap, play the transition over the
   background, then settle on the next stage still.

## Hard/risky parts

- **Transparent output in-browser** — no reliable transparent-WebM / animated-WebP
  encoder in browsers. Robust route: a frame sequence / sprite sheet (~12–15 frames
  for 1s) animated by JS. Reuse the existing in-editor **WebP compressor** to shrink
  each frame.
- **CORS** — gen APIs return a URL; fetching the bytes back into the editor may need
  a small proxy.
- **Cost / latency / non-determinism** — each clip costs credits, takes ~30s–minutes,
  and start→end morphs sometimes need a re-roll. Not instant, not free.

## Recommended phasing

- **Phase 0 — client-side morph (no API).** Canvas cross-fade / warp-dissolve between
  the two stage PNGs during the transform. Delivers "just add images, get a
  transition" with zero cost/key, instant, self-contained. Builds the runtime
  transition plumbing in `buildAd` once. Ships fast, de-risks everything.
- **Phase 1 — generative video API on top,** reusing that plumbing + WebP baking.
  Multi-day, external dependency.

## Candidate APIs (start+end keyframe support)

- **Luma Dream Machine** — explicit start+end keyframes.
- **Runway (Gen-3/4)** — first+last frame interpolation.
- **Kling** — start & end frame.

(Verify current API specifics before building — provider not yet chosen.)

## Open decisions when resumed

- Approach: Phase 0 first (recommended) vs. straight to API vs. client-side only.
- Which video API + whether credits/budget are available.
- Default transition length (1s) and FPS.
- Which stage pairs get transitions (1→2, 2→3, both).
