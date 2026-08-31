---
name: anime-editorial-poster
description: Create refined anime fashion-editorial posters and prompt packages. Use for anime magazine covers, character special-edition posters, or multi-reference image prompts that separately control character, outfit, pose, typography, and lighting; not for chibi art, complex narrative scenes, photography, or dense e-commerce pages.
---

# Anime Editorial Poster

Turn character, outfit, pose, composition, light, and typography inputs into a coherent prompt for a premium anime editorial poster. Preserve the user's explicit requirements; this skill prevents references from bleeding into one another and keeps the result from becoming a generic character illustration or promotional template.

## Visual DNA

- Refined Japanese anime illustration with light semi-cel, restrained painterly rendering; mature and composed rather than chibi or moe.
- A large dominant figure: generally 75–95% frame occupancy, often with a natural editorial crop. Never shrink the character merely to reveal the entire outfit.
- White, warm off-white, or very light warm-gray minimal background. Keep the visual density low.
- One hard directional key light and a crisp, graphic cast shadow. Avoid cinematic volumetric light, haze, neon, or lens flare.
- Oversized high-contrast serif / Didone-inspired editorial typography, a prominent issue number, and sparse supporting text.
- Muted elegant palette. Background is lightest; use at most one strong accent color unless the user asks otherwise.
- Detail control is the default: preserve the character's required outfit construction and recognisable accessories, but organise them into clear value groups and a deliberate hierarchy. Reduce visual noise from all-over micro-texture, repetitive tiny marks, scattered decorative fragments, or equally sharp detail across the character. When a layout reference supplies intentional background texture, halftones, or collage language, retain that graphic texture; do not flatten the background to solve character noise. Large colour and value masses should support the composition, not turn it into flat colour-block art.
- Surface rendering must remain physically and graphically coherent: folds follow fabric tension, gravity, seams, or body contact; highlights describe continuous planes and light direction; hair is organised into clear directional locks. Do not use arbitrary sharp creases, isolated white glints, fragmented hair wisps, or speckled marks as a substitute for form.
- When the layout reference has a strong graphic language, the figure must belong to that system rather than sit on top of it. Carry the layout's palette, edge treatment, shadow geometry, and selected print texture into the figure's non-focal areas; retain clean facial rendering and do not flatten the figure into a poster cutout.

## Editorial Fusion Default

When a supplied layout reference uses a bold graphic system, apply these as the default figure-to-layout bridge unless the user asks otherwise:

- Do not impose a fixed palette or a fixed blue-black-white treatment. First extract the assigned layout reference's own dominant palette, contrast range, geometry, line weight, texture, and type rhythm; then derive the figure treatment from those properties.
- Reuse the layout's strongest accent colour as a restrained rim-light, contour, or cast-side shadow accent on hair and clothing; keep skin and face predominantly natural.
- Echo halftone, print grain, or line treatment only on outer hair masses, garment shadow planes, and non-focal silhouette edges. Keep the face, eyes, hands, and smooth skin clean.
- Align selected background lines, blocks, and shadow directions with the figure's shoulder, waist, hair flow, or garment contours, so the page reads as one composition. Do not let graphics cross the face, hands, or essential costume construction.
- Match the figure's deepest darks and lightest values to the layout palette. Preserve semi-cel depth and material form; this is an integrated editorial illustration, not a flat vector cutout.

Defaults when unspecified: 3:4, slight high angle, mid-thigh or large half-body crop, 85% figure scale, warm off-white background, single hard directional light, a large crisp cast shadow, and a calm restrained expression.

## Resolve Inputs and References

First separate every supplied reference into a responsibility. State both what it contributes and what it must *not* contribute.

- Character reference: identity, face, hairstyle, hair/eye color, signature accessories, and temperament only.
- Outfit reference: garment silhouette, material, construction, and accessory relationships only.
- Pose reference: body pose, camera angle, crop, and figure scale only.
- Layout reference: title placement, issue-number placement, whitespace, and typographic character only.
- Lighting reference: background value, hard-shadow direction, and shadow area only.

Use this precedence for conflicts: current explicit user instruction → stated reference responsibility → character identity → outfit structure → pose/composition → visual DNA → defaults. Do not replace a specified outfit with one from a pose reference, or inherit a reference's face, expression, palette, or character identity unless it was assigned that role.

For style continuation, preserve the style DNA, typography character, lighting logic, palette control, and large-subject principle; do not copy individual reference elements. For multi-reference tasks, define all responsibilities before writing the prompt.

## Character Story and Copy Verification

Treat character identity and story copy as separate facts. Never infer a named character, franchise, relationship, job, or plot point only from visual resemblance. A wrong character name or invented backstory is worse than a neutral editorial line.

1. **Identity lock:** Use the user's explicit character name and franchise first. If either is missing, ask for it when the copy must refer to canon. If the user wants immediate generation, use only visual descriptors and story-neutral copy; do not guess.
2. **Fact basis:** Build copy only from (a) user-provided story facts, or (b) reliable official material when external verification is available and appropriate. Keep a short distinction between canon fact, creative interpretation, and purely decorative text.
3. **Narrative angle:** Reduce the verified material to one emotional tension and one active choice. Good poster copy expresses an arc without reciting a plot summary: constraint → self-definition, isolation → connection, performance → self-expression, or a similar verified contrast.
4. **Copy boundaries:** Do not invent trauma, romance, death, status, dates, band roles, or quotations. Avoid claiming an exact line is canon unless it is verified as such.

Before generating, silently run this preflight:

```text
Identity explicitly confirmed?  yes / no
Franchise explicitly confirmed? yes / no
Story facts supplied or verified? yes / no
Copy mode: canon-informed / character-informed / story-neutral
```

If any answer needed for canon-informed copy is `no`, downgrade to character-informed or story-neutral copy rather than fabricating specificity.

## Typography Delivery Modes

Choose the text-delivery mode before prompting. Image models are suitable for short, visually dominant words but are not dependable for long or legally/commercially exact copy.

- **Concept mode:** Use 1–3 short headlines in the image. The model may render typography artistically; exactness is not guaranteed.
- **Exact-text image mode:** Limit the image to a name, issue number, and one short line. State every required string verbatim and reserve generous, uncluttered type zones.
- **Production-overlay mode (default when exact copy, non-Latin text, or small labels matter):** Generate the visual with clean empty type zones, then provide a post-layout specification: exact strings, hierarchy, placement, alignment, colour, size relationship, and safe margins for Photoshop/Figma/InDesign. Do not force dense paragraphs into image generation.

When the user says “generate text,” write the proposed copy first, label its narrative basis, and use it in the image only at the chosen delivery level. Preserve a separate editable text list even when text is also generated into the artwork.

## Prompt Construction

Build the final generation prompt in this order, using the user's requested language and adapting syntax only when a target model is named:

1. **Style:** minimalist high-fashion anime editorial poster; refined Japanese anime illustration; light semi-cel with restrained painterly rendering; sophisticated magazine-cover design; clean warm off-white background. Preserve material and garment detail where it defines the design, while keeping surfaces clean, linework controlled, and secondary areas visually quiet. Require continuous value planes and directional lighting rather than scattered white highlight flecks. Echo the assigned layout's palette and graphic edge language in the figure's clothing and non-focal shadows so the illustration is integrated with the page.
2. **Character:** name/identity lock, hairstyle, hair and eye color, signature accessories, temperament. Default facial direction: refined mature features, calm restrained gaze, not overly cute.
3. **Outfit:** type, main colour, material, silhouette, and non-negotiable structural details such as neckline, straps, waist, sleeves, hem, or signature hardware. Preserve reference-specific construction, but group secondary texture and decoration into calm, readable areas rather than rendering every surface with equal fine detail. Folds must be broad and purposeful, originating from construction, tension, gravity, or pose; do not add random angular creases or decorative wrinkle noise. Keep it fashion-forward, elegant, restrained, editorial.
4. **Pose and composition:** exact pose and expression, camera angle, crop, approximate occupancy, placement, and permitted out-of-frame crop. Reinforce a large dominant subject (normally 80–90% of frame).
5. **Lighting and background:** single hard directional light, crisp graphic cast shadow, high-key minimalist background. If the layout is graphic, derive and specify its own accent colour, edge treatment, contrast, and limited texture zones that visually fuse the figure into that layout; never substitute a fixed house palette.
6. **Typography:** select the delivery mode; then specify title, issue number, character name, minimal supporting copy, oversized high-contrast serif title, premium editorial hierarchy, restrained negative space, and protected readable zones. For production-overlay mode, prompt for empty zones rather than dense generated text.

When exact commercial copy matters, split the work into two stages: generate the character visual with typography zones and hierarchy, then set final text in a layout tool. Explain that image models may not render long or exact text reliably; do not sacrifice the composition by forcing it.

## Default Negative Constraints

Add or adapt these unless they conflict with the user's request:

```text
no complex background, no neon lighting, no cinematic volumetric light, no lens flare,
no foggy atmosphere, no overly thick painterly texture, no chibi, no overly cute anime face,
no playful moe pose, no messy composition, no cheap promotional poster look,
no cluttered typography, no over-saturated colors, no dramatic VFX, no busy environment,
no low-quality costume detailing, no tiny full-body character, no generic standing character illustration,
no all-over micro-texture, no random decorative fragments, no repetitive high-frequency marks,
no equal-detail treatment across every surface, no ornamental clutter, no fragmented colour treatment,
no random white highlight specks, no disconnected glossy marks, no arbitrary angular wrinkle noise,
no fragmented hair clumps, no noisy flyaway hair, no scribbly linework
```

## Correct Common Failures

- **Figure too small:** add `large dominant subject, character fills most of the poster, 85%–95% frame occupancy, aggressive editorial crop`.
- **Looks like a standard standing illustration:** add `fashion editorial cover composition, oversized typography, graphic cast shadow, asymmetrical magazine layout`.
- **Too thick or oily:** use `lighter semi-cel rendering, restrained painterly shading, reduced specular highlights, clean surfaces`.
- **Too cute:** use `refined mature facial proportions, narrower restrained eyes, calm aloof expression`.
- **Too colorful:** use `muted palette, one accent color only, light neutral background`.
- **Character too noisy or visually fragmented:** use `clear detail hierarchy on the character, clean grouped fabric surfaces, concentrated detail at the face and key garment construction, quiet secondary costume areas, controlled line density, no random micro-texture or decorative scatter`. Preserve intentional background texture and graphic elements from the assigned layout reference. Do not erase requested costume details or reduce the illustration to flat colour blocks.
- **Clothes or hair look AI-generated:** use `fabric folds follow gravity and tension, broad connected fold families, continuous directional highlights, no isolated white specular dots, hair grouped into flowing directional locks, clean silhouette edges, remove random crease and strand noise`. Preserve the requested outfit construction and background graphics.
- **Character looks pasted onto the layout:** use `unify figure and layout through shared palette, graphic shadow shapes, selective halftone or line accents at non-focal clothing edges, and consistent contrast; preserve refined facial rendering and the figure's dimensional volume`. Do not cover the face or hands with layout graphics.
- **Looks like e-commerce:** use `high-fashion editorial typography, Didone-inspired serif, sparse auxiliary text, generous negative space`.
- **Reference bleed:** restate the permitted inheritance and explicitly exclude identity, outfit, expression, and palette from that reference as needed.

## Revision Routing

When revising, identify the primary failure before changing the prompt. Change only the relevant control layer; do not solve every problem by adding more detail.

- **Wrong character or weak likeness:** strengthen only the explicit identity lock: face proportions, hairstyle silhouette, hair/eye colour, signature accessory, and temperament. Remove any conflicting identity cues inherited from other references.
- **Wrong story copy or name:** replace the copy from the verified copy card. Do not regenerate facts from a visual reference; use story-neutral wording if confirmation is still missing.
- **Text is misspelled or unreadable:** switch to production-overlay mode. Regenerate with simple title zones, then place the exact text in a layout tool.
- **Outfit construction drifted:** restate the non-negotiable neckline, straps, sleeve, waist, hem, hardware, and opacity constraints; reduce secondary trims before adding more instructions.
- **Pose, hands, feet, or camera drifted:** isolate the pose reference as the sole source for body geometry and camera. State the exact limb anchors and crop; ask for a pose correction rather than changing identity or outfit.
- **Character has AI noise:** apply the surface-coherence constraints: broad tension-led folds, continuous highlights, grouped hair locks, clean focal face/hands. Keep the approved background print texture.
- **Character looks pasted onto the page:** increase only the layout-to-figure bridge: extract the reference palette, contour treatment, shadow geometry, and limited non-focal print texture; align graphics to the silhouette without crossing face, hands, or essential costume details.
- **Layout no longer resembles its reference:** re-extract the reference's own palette, contrast, grid density, type rhythm, geometry, and texture. Do not revert to a fixed house palette or generic editorial defaults.

## Required Output

Unless the user asks only for a prompt, provide:

1. **Reference mapping** — each image's inherited and excluded elements.
2. **Copy card** — character/franchise confirmation; factual basis; creative angle; final editable strings; and whether each line is canon-informed, character-informed, or story-neutral.
3. **Final generation prompt** — ready to paste into the chosen image model.
4. **Negative constraints / locks** — concise requirements to preserve during generation or revision.
5. **Production overlay plan** — include when typography must be exact: text zones, hierarchy, alignment, colours, and safe margins.

## Quality Check

Before handing off a generated prompt or review, check: explicit identity and franchise confirmation; story claims distinguished from creative copy; editable exact strings preserved outside the image; identity, hair/eye color and signature accessories; outfit construction; hands, legs, straps, and shoes; pose and crop; the intended scale; coherent hard-light direction; clean non-neon background; a magazine hierarchy that does not obstruct the face; a clear large-shape read before any fine detail; folds that follow plausible fabric forces; continuous rather than speckled highlights; and hair that reads as organised locks rather than noise. For a layout-led poster, confirm that its palette and graphic language come from the assigned layout reference rather than a fixed default.

The outcome should read first as a premium anime fashion editorial poster, not a normal character image with text added afterward.
