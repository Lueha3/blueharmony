# Seedance 2.5 — Style Transfer Prompt from Reference Reel

Analysis of the reference reel (a `holydrip.club` styling reel) — its mood, tone,
and style — mapped onto the supplied model photos (Korean man, 170 cm / 65 kg) as a
Seedance 2.5 prompt set.

---

## 1. Reference Video Analysis

### 1-1. Technical Spec

| Item | Value |
|---|---|
| Resolution | 884 × 1920 (vertical 9:16) |
| Frame rate | 30 fps |
| Duration | 63.0s |
| Codec | HEVC / AAC 44.1kHz stereo |
| Audio | No silent gaps up to 62.3s → continuous narration + beat |

### 1-2. Two Layers

The video is made of **two layers**. Separating them is essential, or the prompt
goes off the rails.

**Layer A — screen-recording wrapper (not a reproduction target)**
An iPhone screen recording of an Instagram Reel.
Status bar (9:45, 100% battery), the red Dynamic Island recording dot, the
"Reels / Friends" tab, the right-side like/comment(1,315)/share(6,999) icons, the
bottom navigation bar, the `holydrip.club` account and the caption
"The CEO has been cooking with his looks ✨".

→ **This must not be AI-generated.** Text and icons will break.
   If needed, composite a real UI mockup on top in an editing tool instead.

**Layer B — the actual reel content (the reproduction target)**
A **chapter-based styling tutorial** featuring a plus-size male model.
`#1 FABRICS → #2 COLLARS → #3 LAYERING → #4 SHOES → #5 EYEWEAR`

### 1-3. Mood / Tone / Style

**Space**
- Seamless infinite white cyclorama. Zero props, furniture, or walls
- A very faint cool-grey gradient toward the corners
- One soft contact shadow under the feet — the only thing keeping him from
  looking like he's floating

**Lighting**
- High-key. Large frontal softbox plus even fill
- Almost no shadow on the face, flat even skin tone
- A small soft catchlight on the glasses lenses
- Exactly the lighting of a commerce lookbook / e-commerce product shoot

**Camera**
- Locked-off tripod, zero handheld shake
- Eye-level, dead-on frontal framing, an undistorted ~50 mm field of view
- Default is a **full-body wide shot** (generous headroom)
- Intercut with bust close-ups, face close-ups, and lower-body detail shots
  (pants + shoes)
- Movement is limited to a very slow push-in

**Editing**
- Hard cuts on the beat. Each look holds for **1-2 seconds**
- The signature move is the **wardrobe teleport** — a match cut where pose and
  framing stay fixed and only the clothes swap instantly
- No transition effects (dissolves, wipes). Cuts only

**Graphics (the video's real identity)**
- Uppercase geometric sans-serif. Pure white or charcoal only
- Chapter titles: a large uppercase word with a small tracked-out `HACK 4` above it
- **Pill-shaped white badges with a red ❌ / green ✅**
  `❌ SLIM` `✅ CHUNKY SHOES` `❌ THIN FABRIC` `✅ CREW NECK` `✅ WIDE LAPELS`
- **Black dashed-line diagrams** — shoulder line, face-outline oval, length
  markers, `longer`, `stronger base`
- **A vertical swatch picker on the right edge** —
  `COTTON / DENIM / TWILL / LINEN / CO-ORD` with a cursor clicking through them
- Intro: a stack of white rounded cards (thumbnail + chapter name + `#1`–`#5`)

**Color grade**
- Bright and neutral. Low contrast, accurate white balance
- Background and graphics are fully desaturated → **saturation lives only in
  the clothing**
- Crisp and digital. No film grain

**Overall feel, in one line**
> A fashion tutorial that looks like a premium app onboarding screen. Deadpan,
> no humor, taught with quiet confidence. A soft-sell "before → after glow-up."

---

## 2. Applying the Model

### 2-1. The Person in the Photos

- Korean man, early-to-mid twenties
- 170 cm / 65 kg → **lean, balanced build**. Narrow-ish shoulders, no excess
- Black hair, two-block cut with a soft side-swept fringe, slight wave and
  volume on top
- **Thick black acetate round (Boston) glasses** — the defining feature
- Fair skin, clean jawline, straight nose, small full lips
- Expression ranges from calm neutral to a faint smile

### 2-2. ⚠️ Why the Content Logic Has to Flip

The original model is plus-size, so every chapter is about
**"how to dress around your build"** — thin fabrics, crew necks, chunky shoes to
stabilize the lower body.

Applying that same logic to a slim 170 cm / 65 kg build doesn't hold up.
The chapters should flip to **"how to build volume and proportion on a slim
build."**

| Original chapter | Ported chapter | Logic |
|---|---|---|
| #1 FABRICS (thin fabric) | **#1 PROPORTION** | Shorts that cut off cleanly at the knee → bare shin reads longer legs |
| #2 COLLARS (small collar ❌) | **#2 VOLUME** | An oversized top compensates for narrow shoulders |
| #3 LAYERING | **#3 LAYERING** | A grey puffer builds upper-body bulk |
| #4 SHOES (chunky) | **#4 SHOES** | Chunky sneakers add lower-body weight and height |
| #5 EYEWEAR | **#5 EYEWEAR** | Keep the round glasses, compare frame thickness |

### 2-3. The Specified Outfit

Three real products the user specified. The prompt describes them by
**shape, material and color only, with no brand name** — feeding a brand name to
the generation model makes it invent a logo and stamp it onto the frame.

| Item | Prompt description |
|---|---|
| **Grey wide-leg shorts** (Nande shorts) | Heather marled light grey brushed sweat fabric, voluminous A-line cut, a pressed centre crease down the front, elastic waistband with a grey drawstring, slanted side pockets, hem ending right at the knee |
| **Chunky sneakers** | Off-white cream leather upper, pale grey wavy overlay panels on the sides, white round laces, a very tall layered lugged midsole |
| **Light down jacket** (BlackYak Stonemaster) | Pale ice-grey silver, glossy ripstop nylon, horizontal quilted baffle channels on body and sleeves, full-length grey zip, puffed hood with visible black lining, two zippered hand pockets, slim rather than bulky |

Paired with an **oversized white crew-neck tee** (dropped shoulder, hip-length
hem) and **white ribbed crew socks** (pulled to mid-calf).

> The shorts + puffer combo was kept as intentional. It's not a seasonal clash —
> it's a common layering choice in Korean streetwear, so it was left as-is.

---

## 3. Seedance 2.5 Prompts

> **Length constraint**: Seedance 2.5 caps at 30 seconds per call.
> The source is 63 seconds, so generating **segments and stitching them in an
> editing tool** is recommended. Below is an 8-second × 5-segment structure.

### Shared Anchor Block

Prepend this block to every segment prompt. It's the backbone of subject
consistency.

```
SUBJECT ANCHOR — keep identical in every shot:
A slim young Korean man in his early twenties, matching the reference image exactly:
fair skin with a warm undertone, clean-shaven, a slender oval face with a defined
jawline, a straight nose and small full lips. Black two-block haircut — tapered
short sides, soft side-swept fringe, slight wave and volume on top. He wears thick
round black acetate glasses (Boston-style frames) at all times. Lean athletic build,
170 cm and 65 kg: narrow shoulders, flat stomach, no bulk, long clean limbs.
Calm neutral expression, quiet confidence, no exaggerated smiling.

WARDROBE ANCHOR — the hero outfit, reproduce these garments exactly:
- Top: an oversized white crew-neck T-shirt in heavy cotton, boxy cut with dropped
  shoulder seams, worn untucked, the hem falling to the upper hip.
- Bottom: wide-leg knee-length sweat shorts in heather marled light grey brushed
  fleece. Very voluminous A-line cut, a sharp pressed centre crease running down the
  front of each leg, an elastic waistband with a matching grey drawstring, and
  slanted side pockets. The hem ends right at the knee.
- Socks: plain white ribbed cotton crew socks pulled up to mid-calf.
- Shoes: chunky retro "dad" runner sneakers in off-white cream leather, with pale
  grey wavy overlay panels along the sides, white round laces, and a very tall
  layered lugged midsole.
- Outerwear (only in shots that call for it): a lightweight hooded down puffer
  jacket in pale ice-grey silver, glossy ripstop nylon with a soft sheen, horizontal
  quilted baffle channels across the body and sleeves, a full-length matching grey
  front zip, an attached puffed hood with black lining visible at the opening, and
  two zippered hand pockets. Slim and packable, not bulky.

STYLE ANCHOR — keep identical in every shot:
Seamless infinite white studio cyclorama, absolutely no props, furniture or visible
walls, faint cool-grey falloff in the corners, one soft contact shadow pooling under
his shoes. High-key lighting: a large frontal softbox plus even fill, almost no
shadow on the face, flat even skin, a small soft catchlight in each glasses lens.
Locked-off tripod, eye-level, 50 mm lens, dead-on frontal framing, zero handheld
shake. Bright neutral grade, low contrast, accurate white balance, fully desaturated
background — colour exists only in the clothing. Crisp digital sharpness, no film
grain, no vignette, no lens flare. Vertical 9:16 e-commerce lookbook aesthetic.
```

---

### SEG 1 — INTRO / Menu (8s)

```
[SUBJECT ANCHOR] [STYLE ANCHOR]

Full-body wide shot, head-to-toe with generous headroom. He stands centered, feet
shoulder-width apart, arms relaxed at his sides, facing camera dead-on, wearing the
full hero outfit from the WARDROBE ANCHOR — oversized white tee, heather grey
wide-leg knee-length sweat shorts, white crew socks, chunky cream sneakers. No
jacket yet.

Motion: he holds the pose almost perfectly still — one natural breath, one slow
blink, a barely perceptible weight shift. The camera performs one extremely slow
push-in across the full 8 seconds.

Graphics: flat 2D motion-design overlays composited over the shot, crisp uppercase
geometric sans-serif in pure white and charcoal only. Four white rounded-rectangle
cards slide up from the bottom one after another, evenly stacked, each with a small
square garment thumbnail on its left edge and a large uppercase label:
"PROPORTION", "VOLUME", "LAYERING", "SHOES".

No text distortion, no watermark, no UI chrome, no phone interface.
```

---

### SEG 2 — PROPORTION / High-waist Comparison (8s)

```
[SUBJECT ANCHOR] [STYLE ANCHOR]

Full-body wide shot, identical framing and identical pose throughout.

Beat 1 (0-3s): he wears a long baggy white T-shirt hanging past his hips over full-
length loose grey sweatpants that puddle over flat low-profile sneakers — the leg
line is swallowed and his height reads short.
Beat 2 (3-8s): hard cut on the beat, a wardrobe teleport — the pose, framing and
lighting stay EXACTLY the same, only the clothes change instantly. Now the hero
outfit: the boxy oversized white tee ending at the upper hip, heather grey wide-leg
sweat shorts cut off right at the knee, white ribbed crew socks and the chunky cream
sneakers, so bare shin shows between hem and sock and the leg line reads longer.

Motion: minimal. He stays planted, breathing naturally, a single blink per beat.

Graphics: a small white pill-shaped badge with a red cross icon reading "LOW RISE"
appears at his waist in beat 1; on the cut it is replaced by a white pill badge with
a green check reading "HIGH WAIST". A thin black dashed horizontal guide line marks
the waistline in both beats. A small tracked-out label "HACK 1" sits above a large
uppercase title "PROPORTION" in the upper third.

No text distortion, no watermark, no UI chrome, no phone interface.
```

---

### SEG 3 — VOLUME / Oversized Fit (8s)

```
[SUBJECT ANCHOR] [STYLE ANCHOR]

Medium shot framing him from mid-thigh up, then holding.

Beat 1 (0-4s): a tight slim-fit white T-shirt that clings to his narrow frame and
emphasises how slight his shoulders are, worn with the heather grey wide-leg shorts.
Beat 2 (4-8s): hard cut, wardrobe teleport with identical pose and framing — the
same grey shorts, but now the oversized white crew-neck tee from the WARDROBE
ANCHOR, boxy with dropped shoulder seams and a wide body, instantly giving him
breadth.

Motion: he lifts his chin very slightly on the cut, then settles. Nothing else moves.

Graphics: thin black dashed lines trace the outline of his shoulders in both beats,
widening visibly on the second. A white pill badge with a red cross reads "SLIM FIT"
in beat 1, replaced by a green-check white pill badge reading "DROPPED SHOULDER".
Small tracked-out "HACK 2" above a large uppercase "VOLUME".

No text distortion, no watermark, no UI chrome, no phone interface.
```

---

### SEG 4 — LAYERING / Swatch UI (8s)

```
[SUBJECT ANCHOR] [STYLE ANCHOR]

Full-body wide shot, locked off, identical pose held throughout.

He wears the hero base — oversized white tee, heather grey wide-leg knee-length
sweat shorts, white crew socks, chunky cream sneakers. On the beat, the pale
ice-grey hooded down puffer jacket appears on him in a single frame: glossy ripstop
nylon with a soft sheen, horizontal quilted baffle channels across body and sleeves,
a full-length matching grey front zip worn open, an attached puffed hood with black
lining visible at the opening, two zippered hand pockets, slim and packable rather
than bulky. Pose, framing and lighting stay perfectly unchanged; every other garment
is untouched. It zips up halfway on the next beat, then the hood goes up on the last.

Motion: he keeps his hands loosely at his sides and stays still; only the jacket
changes create movement.

Graphics: three small square swatch cards stack along the right edge of the frame,
labelled in tiny uppercase — "OPEN", "ZIPPED", "HOOD UP" — and a small white cursor
arrow clicks each in turn, a green check mark popping onto the card as the jacket
changes on him. Small tracked-out "HACK 3" above a large uppercase "LAYERING".

No text distortion, no watermark, no UI chrome, no phone interface.
```

---

### SEG 5 — SHOES + EYEWEAR (8s)

```
[SUBJECT ANCHOR] [STYLE ANCHOR]

Beat 1 (0-4s): tight detail shot cropped from the knees down — the heather grey
fleece shorts hem at the knee, bare shins, white ribbed crew socks. Flat thin-soled
canvas sneakers first, then a hard cut to the chunky cream "dad" runners with their
tall layered lugged midsole and pale grey wavy side panels. Same shorts, same socks,
same camera position, same floor shadow.
Beat 2 (4-8s): hard cut to a tight head-and-shoulders close-up, eye-level, dead-on.
He wears the thick round black acetate glasses, with the grey puffer collar just
visible at the bottom of frame. Very slow push-in.

Motion: in the close-up he blinks once, then gives a small closed-mouth smile in the
final second.

Graphics: in beat 1, a white pill badge with a red cross reads "THIN SOLE",
replaced on the cut by a green-check badge reading "CHUNKY". In beat 2, a thin black
dashed oval traces the outline of his face, and a green-check white pill badge reads
"ROUND FRAME". Small tracked-out "HACK 4 / 5".

No text distortion, no watermark, no UI chrome, no phone interface.
```

---

### Single-call version (15s, for quick validation)

If five segments feel like too much, use this one to check the tone first.
The **copy-paste-ready version, with the anchors merged inline, is in section
4-1**. Its shot structure:

| Shot | Time | Content |
|---|---|---|
| 1 | 0-4s | Full-body wide shot. Hero outfit (oversized white tee + grey wide-leg shorts + white socks + chunky sneakers), no jacket |
| 2 | 4-8s | Hard-cut wardrobe teleport. Pose and framing unchanged, **only the grey puffer is added** |
| 3 | 8-11s | Below-the-knee detail shot. Shorts hem, bare shin, white crew socks, chunky sole |
| 4 | 11-15s | Face close-up. Very slow push-in, a faint smile on the final beat |

---

### Clean-plate version (no graphics — recommended)

AI text rendering is unreliable. **Generating a clean plate with no graphics, then
adding captions/badges/dashed lines in an editing tool** (After Effects / CapCut)
gives the highest-quality result.

Delete the entire `Graphics:` paragraph from the prompts above and replace the
final line with:

```
Completely clean frame: no text, no captions, no badges, no logos, no watermark,
no user interface elements of any kind.
```

---

## 4. Call Parameters

```json
{
  "model": "seedance_2_5",
  "prompt": "<prompt above>",
  "params": {
    "mode": "omni_reference",
    "aspect_ratio": "9:16",
    "duration": 8,
    "resolution": "720p",
    "generate_audio": false,
    "medias": [
      { "role": "image_references", "value": "<photo1 media_id>" },
      { "role": "image_references", "value": "<photo2 media_id>" },
      { "role": "image_references", "value": "<photo3 media_id>" }
    ]
  }
}
```

**Rationale for each setting**

| Parameter | Value | Reason |
|---|---|---|
| `mode` | `omni_reference` | Needs to carry the facial identity from the photos |
| `aspect_ratio` | `9:16` | Matches the source's vertical reel, 884×1920 |
| `duration` | `8` | Per segment. Up to 30s is allowed |
| `resolution` | `720p` | Seedance 2.5's ceiling (only 480p/720p supported) |
| `generate_audio` | `false` | The source uses narration + a beat; better to add audio separately with full control |
| `medias` | 3 front/side photos | More angles keep identity more stable |

**Cautions**
- Seedance 2.5 **caps at 720p**, lower than the source (884×1920).
  For higher resolution, consider `seedance_2_0` (std mode, up to 4K) or
  `minimax_h3` (2K), or run `upscale_video` after generation.
- Wardrobe teleports are safe up to **2-3 per segment**.
  Push past that and the face starts to drift.
- Keep on-screen text per frame to **one block, uppercase, two words or fewer**.

---

## 4-1. Running It Directly on the Higgsfield Website (copy-paste)

### Steps

1. Log into **higgsfield.ai** → go to Video / Generate
2. **Select the `Seedance 2.5` model**
   - Seedance 2.0 / 2.0 Mini also appear in the model list. Make sure to pick **2.5**
3. **Upload the reference images** — all 3 photos with the browser chrome cropped out
   - If there's a role selector, set it to **`image_references`**
   - It must NOT be assigned to `start_image` — that would bake the photo's
     background (a hallway/classroom) straight into the first frame
4. **Set mode to `omni_reference`** (usually switches automatically once
   references are uploaded)
5. Enter the settings below, then paste the prompt

### Settings

| Field | Value |
|---|---|
| Model | `Seedance 2.5` |
| Mode | `omni_reference` |
| Aspect ratio | `9:16` |
| Duration | `15` |
| Resolution | `720p` (2.5's ceiling) |
| Generate audio | **off** |

### Prompt (copy the whole block)

```
A slim young Korean man in his early twenties, matching the reference photos
exactly: fair skin with a warm undertone, clean-shaven, a slender oval face with a
defined jawline, a straight nose and small full lips. Black two-block haircut —
tapered short sides, a soft side-swept fringe, slight wave and volume on top. He
wears thick round black acetate glasses (Boston-style frames) in every shot. Lean
build, 170 cm and 65 kg: narrow shoulders, flat stomach, no bulk, long clean limbs.
Calm neutral expression, quiet confidence, no exaggerated smiling.

His outfit, reproduced exactly in every shot: an oversized white crew-neck T-shirt
in heavy cotton, boxy with dropped shoulder seams, worn untucked with the hem
falling to the upper hip. Wide-leg knee-length sweat shorts in heather marled light
grey brushed fleece — very voluminous A-line cut, a sharp pressed centre crease down
the front of each leg, an elastic waistband with a matching grey drawstring, slanted
side pockets, the hem ending right at the knee. Plain white ribbed cotton crew socks
pulled up to mid-calf. Chunky retro "dad" runner sneakers in off-white cream
leather, with pale grey wavy overlay panels along the sides, white round laces and a
very tall layered lugged midsole.

Setting and look, identical in every shot: a seamless infinite white studio
cyclorama, absolutely no props, furniture or visible walls, a faint cool-grey
falloff in the corners, and one soft contact shadow pooling under his shoes.
High-key lighting — a large frontal softbox plus even fill, almost no shadow on the
face, flat even skin, a small soft catchlight in each glasses lens. Locked-off
tripod, eye-level, 50 mm lens, dead-on frontal framing, zero handheld shake. Bright
neutral grade, low contrast, accurate white balance, a fully desaturated background
so colour exists only in the clothing. Crisp digital sharpness, no film grain, no
vignette, no lens flare. Vertical 9:16 e-commerce lookbook aesthetic.

A 15-second fashion styling tutorial reel, cut hard on the beat.

Shot 1 (0-4s): full-body wide shot, head to toe with generous headroom. He stands
dead-on, arms relaxed at his sides, feet shoulder-width apart, wearing the outfit
above. He is almost perfectly still — one natural breath, one slow blink.

Shot 2 (4-8s): hard cut, a wardrobe teleport — the pose, framing, lighting and every
other garment stay EXACTLY the same, and a jacket simply appears on him between one
frame and the next. Over the white T-shirt he now wears a lightweight hooded down
puffer jacket in pale ice-grey silver: glossy ripstop nylon with a soft sheen,
horizontal quilted baffle channels across the body and sleeves, a full-length
matching grey front zip worn open, an attached puffed hood with black lining visible
at the opening, and two zippered hand pockets. Slim and packable, not bulky. The
grey shorts, white socks and chunky cream sneakers are unchanged.

Shot 3 (8-11s): hard cut to a detail shot framed from the knees down — the wide
fleece shorts hem falling at the knee, bare shins, white ribbed crew socks, and the
tall lugged midsoles of the cream sneakers planted on the white floor with a soft
contact shadow.

Shot 4 (11-15s): hard cut to a tight head-and-shoulders close-up, eye-level,
dead-on, the thick round black glasses catching a small soft highlight, the grey
puffer collar just visible at the bottom of frame. Extremely slow push-in. He blinks
once and gives a small closed-mouth smile on the final beat.

Completely clean frame: no text, no captions, no badges, no logos, no watermark,
no brand marks on any garment, no user interface elements of any kind.
```

### What to check in the result

This 15-second clip is for judging five things.

1. **Is the face the same person as the photos?** — check shot 4's close-up
   especially
2. **Is the background a seamless white infinity?** — a leak of the photo's
   hallway/classroom means failure
3. **Does the pose hold through the cut while only the puffer gets added?** —
   the wardrobe teleport is the core of this video
4. **Did the outfit come out as specified?** — does the shorts hem cut off at
   the knee, is the sneaker sole thick enough, is the puffer's quilting
   horizontal
5. **Is the lighting flat and high-key?** — a shadow on the face means the tone
   is off

| Failure point | Fix |
|---|---|
| #1 | Crop the reference photos tighter around the face and re-upload |
| #2 | The photo was likely assigned to `start_image`. Check the role |
| #3 | Cut down to 2 shots and set duration to 10s |
| #4 | Upload a product shot of that item **in addition**, into `image_references`. If mixing it with the portrait photos destabilizes the face, run a separate outfit-only pass and pick the better result |

---

## 5. Points to Confirm

1. **What the landscape screenshot is for (man in a denim shirt, closet background)**
   It's a different scene from the uploaded video. The prompts above lock in the
   three vertical photos as the model reference. If that closet setting (a
   walk-in closet with clothes on white hangers) should also be reproduced,
   swap the white cyclorama in `STYLE ANCHOR` for that closet.

2. **Whether to reproduce the Instagram UI**
   If the screen-recording wrapper is also wanted, the right approach is a real
   UI mockup composited in an editing tool, not AI generation.

3. **Audio**
   The source has continuous narration + a beat for the full 63 seconds. If a
   Korean narration script is needed, it can be written separately to match the
   chapter structure.
