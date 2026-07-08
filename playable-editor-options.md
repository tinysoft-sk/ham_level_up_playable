# Magic War Legends — Playable Ad Editor: Full Options Reference

This document describes every control available in the editor.
Use it to instruct an AI (e.g. Gemini) to generate scenario configs for playable ads.

---

## How the Editor Works

The ad is a single-page HTML5 playable built around a **tap-to-level-up** mechanic:

1. Player sees the base unit (Stage 1) with a star progress bar and a tap hint.
2. Each tap fills one or more stars and plays a click sound.
3. When all taps are done, the unit **transforms** (particle burst, screen shake, flash) and the leveled-up unit is revealed.
4. The CTA button appears, optionally with a stats card and/or outro animation.

Up to **3 stages** are supported (Stage 1 → Stage 2 → Stage 3).
An optional **Intro scene** plays before the game; an optional **Outro scene** plays after the transform.

All assets are embedded as base64 data URIs — the exported file is fully self-contained.

---

## Tab: 📦 Assets

### ⚔️ Stage 1 — Base Unit

| Field | Type | Notes |
|-------|------|-------|
| Unit Still Image | Image upload | PNG with transparency recommended. ~400×600 px. Accepts image/*. Saved to asset library automatically. |
| Unit Size | Slider 20–100% | Max width as % of screen. Separate values for portrait and landscape. |

### ✨ Stage 2 — Level Up *(required)*

| Field | Type | Notes |
|-------|------|-------|
| Stage 2 Asset | Image or video upload | PNG, GIF, Animated WebP, MP4, WebM. Revealed on transformation. |
| Leveled-Up Size | Slider 20–100% | Applied after transformation. Per-orientation. |
| Edge Blend | Slider 0–90% | Fades edges of the leveled-up image into the background. 0 = off. |
| Reveals at Tap | Number input | Which tap number triggers Stage 2. Default: final tap. |

### ⭐ Stage 3 — Final Form *(optional)*

| Field | Type | Notes |
|-------|------|-------|
| Stage 3 Asset | Image or video upload | PNG, GIF, Animated WebP, MP4, WebM. Second transformation. |
| Stage 3 Size | Slider 20–100% | Per-orientation. |
| Edge Blend | Slider 0–90% | 0 = off. |
| Reveals at Tap | Number input | Must be a tap after Stage 2's tap. |

### 🎨 Branding & Logo

| Field | Type | Notes |
|-------|------|-------|
| Game Logo | Image upload | PNG with transparency. Shown above the star bar. |
| Logo Size | Slider 10–75% | Percentage of screen width. Per-orientation. |
| Store / CTA URL | URL input | App Store or Play Store link. Used by Unity, AppLovin, and the preview CTA button. |

### 🌄 Background

| Field | Type | Notes |
|-------|------|-------|
| Portrait Background | Image upload | 360×640 px recommended. |
| Landscape Background | Image upload | 640×360 px recommended. Both orientations are optional — upload one or both; the ad swaps automatically. |
| Background Vignette | Slider 0–100% | Darkens edges and bottom for text readability. 0 = off. |

### 🎬 Intro Scene *(optional)*

| Field | Type | Notes |
|-------|------|-------|
| Intro Animation | Animated image upload | Animated WebP, GIF. Full-screen before the game starts. Player can tap to skip. |
| Intro Size | Slider 40–100% | 100% = full-screen cover. Lower = centred with letterbox. Per-orientation. |
| Auto-advance after | Slider 2–10 s (0.5 step) | How long the intro plays before auto-advancing to the game. |

### 🏁 Outro Scene *(optional)*

| Field | Type | Notes |
|-------|------|-------|
| Outro Animation | Animated image upload | Animated WebP, GIF. Fades in after the level-up animation. CTA button floats on top. |
| Outro Size | Slider 40–100% | 100% = full-screen cover. Per-orientation. |

### 🔊 Sounds *(optional)*

| Field | Type | Notes |
|-------|------|-------|
| Click / Tap Sound | Audio upload | Plays on every tap. MP3, OGG, WAV. Keep under 200 KB for Facebook. |
| Level Up Sound | Audio upload | Plays on transformation. Same format notes. |

---

## Tab: ⭐ Game

### ⭐ Stars & Taps

| Field | Type | Notes |
|-------|------|-------|
| Star Steps | Visual row of tap/fill boxes | Defines exactly how many stars fill on each tap. Drag steps to redistribute. Default: 1 star per tap across 5 taps. |
| Total ★ shown | Number input | Total star count displayed (can exceed the filled count to leave stars unfilled). |
| Taps | Display only | Derived from the number of steps in Star Steps. |
| Cliffhanger | Number input 0–20 | Fire the CTA early while N stars are still unfilled. Creates urgency. 0 = off (classic flow). |

### 📊 Stats Card *(optional)*

Revealed together with the CTA button after transformation.

| Field | Type | Notes |
|-------|------|-------|
| Enable stats card | Toggle | Shows a character stats panel after level-up. |
| Card Style | Button choice | **Game** (golden RPG frame) or **Minimal** (dark flat). |
| Display Mode | Button choice | **After Level-Up** (appears with CTA) or **Always Visible** (shown from the start, bonuses reveal on level-up). |
| Auto-position above CTA | Toggle | Automatically stacks the card above the CTA button. |
| Bottom Offset | Slider 0–400 px | Manual position when auto is off. |
| Card Scale | Slider 60–140% | Overall size of the stats card. |
| Drag to reposition | Drag in preview | Drag the stats card in the live preview to set an exact position. |
| Stats Rows | Repeatable rows | Each row: Icon (emoji), Label (text), Value (text), +Bonus (text), % growth per tap (number). Up to any count. Examples: ⚡ Power 6.5M +626k, ❤️ Health 29,000 +3,000. |
| Abilities / Badges | Repeatable rows | Each badge: Icon (emoji) + Name (text). Shown as small chips at the bottom of the card. |

### 🏆 End Game Panel *(optional)*

Full-screen competition results overlay that appears when the CTA fires.

| Field | Type | Notes |
|-------|------|-------|
| Enable End Game Panel | Toggle | Shows a game-native results screen on CTA click. |
| Panel Title | Text input (max 30 chars) | e.g. "COMPETITION FINISHED" |
| Result Line | Two text inputs | Label + number, e.g. "You Finished:" + "5" |
| Reward 1 | Icon image upload + value text | Small reward icon with numeric value (e.g. trophy icon + "310"). |
| Reward 2 | Icon image upload + value text | Second reward, same structure (e.g. coin icon + "500"). |

---

## Tab: 🎨 Style

### 📝 Text & CTA

| Field | Type | Notes |
|-------|------|-------|
| Tap Hint Text | Text input (max 40 chars) | The prompt shown below the unit. Default: "TAP TO LEVEL UP!" |
| Tap Hint Color | Color picker | Default: white. |
| Tap Hint Size | Slider 60–160% | Relative to base size. |
| Level Up Banner | Text input (max 30 chars) | The big text that pops up on transformation. Default: "★ LEVEL UP! ★" |
| Level Up Banner Color | Color picker | Default: gold (#ffd700). |
| Level Up Banner Size | Slider 60–160% | |
| Level Up Banner Vertical Position | Slider 20–80% | % from top of screen. Move up if it overlaps the unit. Default: 50%. |
| CTA Button Text | Text input (max 25 chars) | Default: "PLAY NOW — FREE" |
| **Custom Button Image** | Image upload (optional) | PNG with transparency. When set, replaces the styled text button with the image. Color/size/shape controls hide automatically. Button position slider remains active. |
| Button Color | Swatch picker | Presets: Orange, Blue, Green, Purple, 🎮 Game Green, 🎮 Game Orange. Plus a Custom option with separate Background + Text color pickers. Hidden when custom image is set. |
| Button Size | Slider 60–140% | Hidden when custom image is set. |
| Button Shape | Button choice | **Pill** (fully rounded) or **Rounded** (10 px radius). Hidden when custom image is set. |
| Button Position (bottom offset) | Slider 0–120 px | Distance from the bottom edge. Always visible. |

### 🔤 Fonts

| Field | Type | Notes |
|-------|------|-------|
| Font Style | Button choice | **Default** (system UI), **Impact**, **Georgia**, **Custom ↑** |
| Custom Font File | File upload | .woff, .woff2, .ttf, .otf. Recommended under 200 KB. Appears when Custom is selected. |

Applied to: tap hint, level-up text, and CTA button text.

### 📐 Layout & Positions

| Field | Type | Notes |
|-------|------|-------|
| Drag to reposition | Drag in preview | Drag logo, unit, stars, hint text, or stats card in the live preview. Edits the currently selected orientation (portrait or landscape). |
| Exact X/Y fields | Number inputs (0–100%) | Fine-tune element positions numerically. |
| Copy Portrait → Landscape | Button | Copies all positions and sizes from portrait to landscape layout. |
| Copy Landscape → Portrait | Button | Reverse copy. |
| Reset current orientation | Button | Resets positions to default for the active orientation. |

### 🎆 Transformation Effects

| Field | Type | Default | Notes |
|-------|------|---------|-------|
| Particle burst | Toggle | On | Confetti-style burst on transformation. |
| Particle Color Theme | Swatch | Gold | Gold, Fire, Ice, Mystic, Rainbow. |
| Particle Count | Slider 20–120 | 60 | Number of particles. |
| Particle Speed | Slider 50–200% | 100% | Spread speed. |
| Screen shake | Toggle | On | Device shake animation on transformation. |
| Screen flash | Toggle | On | Full-screen color flash on transformation. |
| Unit glow after level-up | Toggle | Off | Adds a glow filter to the leveled-up unit. |
| Flash Color | Swatch + custom picker | White | White, Gold, Sky, Mystic, or any custom color. |
| Flash Intensity | Slider 0–100% | 92% | Peak opacity of the flash. |

---

## Tab: 📡 Export

### 📡 Network Options

| Field | Type | Notes |
|-------|------|-------|
| Playable Name | Text input | Filename prefix for all exports. Converted to a URL-safe slug. Default: "magic-war-legends". Example: "warrior-clash" → `warrior-clash-facebook.html`. |
| Responsible Play footer | Toggle | Adds "18+ \| Play Responsibly \| gamblingtherapy.org" footer. Applied to the **Google** export only. For gambling game advertisers. |

### Export Buttons

| Button | Output format | Network-specific behavior |
|--------|--------------|--------------------------|
| 📘 Facebook | `{name}-facebook.html` | Self-contained HTML. FbPlayableAd.onCTAClick() used for CTA. Max recommended size: 2 MB. |
| 🔴 Google | `{name}-google.zip` | ZIP containing `index.html`. Includes ExitApi script and ad.size meta tags. |
| ⬛ Unity / AppLovin | `{name}-unity-applovin.html` | MRAID 2.0 compliant. Game initializes on viewableChange. CTA uses mraid.open(). |
| 🟡 Mintegral | `{name}-mintegral.zip` | ZIP containing `{name}/index.html` in a named subfolder. Implements gameReady / gameStart / gameClose lifecycle. |

---

## Asset Library

All uploaded assets are saved automatically to an in-browser IndexedDB library, organized by category. You can reuse them across sessions without re-uploading.

Categories: Stage 1 Unit, Stage 2, Stage 3, Logo, BG Portrait, BG Landscape, Intro GIF, Outro GIF, Click Sound, Level Sound, Button Image.

---

## Presets

Save the full editor state as a named preset (💾 Save button in the preset bar). Restore any preset from the dropdown. Presets survive page refresh.

---

## Per-Orientation Layout

Portrait (📱) and Landscape (📺) are edited independently:

- Switch the preview orientation toggle above the phone preview.
- Unit size, leveled-up size, Stage 3 size, logo size, intro/outro size, and all element X/Y positions are stored separately per orientation.
- The background image can differ per orientation.
- Use the Copy buttons (Layout tab) to mirror one orientation to the other as a starting point.

---

## File Size Guide

The size indicator in the preview bar shows the estimated export size:

| Size | Status |
|------|--------|
| Under ~1.5 MB | ✅ All networks OK |
| ~1.5–2 MB | ⚠️ Near Facebook 2 MB limit |
| 2–5 MB | ⚠️ Over Facebook limit — OK for other networks |
| Over 5 MB | ❌ Too large — compress assets |

Largest contributors: background images, unit images, intro/outro animations, audio files.

---

## Scenario Cheat-Sheet for AI Prompting

When asking Gemini (or any AI) to design a playable scenario, describe:

1. **Game genre / theme** — what the unit looks like, what "leveling up" means
2. **Number of taps** — how many taps before the transform (typically 3–7)
3. **Stages** — 2 stages only, or add a Stage 3 dramatic reveal
4. **Cliffhanger** — yes/no; fire CTA while 1–2 stars remain unfilled
5. **Intro scene** — yes/no; what action to show (battle, cinematic, etc.)
6. **Outro scene** — yes/no; what to tease after the transform
7. **Stats card** — yes/no; which stats to show (Power, Health, Attack, Defense, Speed, etc.); "Always visible" or "After level-up"
8. **End Game Panel** — yes/no; what competition result to show
9. **Sounds** — tap sound style (sword clash, coin, magic), level-up sound style (fanfare, explosion)
10. **Tone** — urgency (cliffhanger), epic (full transform), casual
11. **CTA text** — e.g. "PLAY NOW — FREE", "JOIN THE BATTLE", "UPGRADE NOW"
12. **Target networks** — Facebook, Google, Unity, Mintegral (affects file size budget)
