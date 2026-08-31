# Anime Editorial Poster

A reusable Codex skill for creating anime fashion-editorial posters from separate character, outfit, pose, layout, lighting, and copy references.

It is built for character-special posters and magazine-cover artwork where the figure must belong to the layout system—not look like an illustration pasted over a background.

## What it controls

- Reference-role separation: character identity, outfit construction, pose/camera, layout, and lighting do not bleed into each other.
- Editorial fusion: the figure derives palette, contrast, contour treatment, shadows, and selected print texture from the assigned layout reference.
- Surface cleanup: fabric folds, highlights, and hair remain structured and intentional while approved background print texture is preserved.
- Story-safe copy: character names and canon claims are verified before use; unknown details fall back to character-informed or story-neutral copy.
- Reliable typography handoff: exact strings can be delivered as an editable overlay plan instead of relying on an image model to render dense text correctly.
- Targeted revisions: specific repair routes for likeness, copy, clothing, pose, AI noise, layout fusion, and typographic failure.

## Install

Copy or clone this folder into your local Codex skills directory, then restart or refresh the skills environment.

```text
~/.codex/skills/anime-editorial-poster/
├── SKILL.md
└── agents/openai.yaml
```

The public repository intentionally contains no user-uploaded images, copyrighted character art, generated poster outputs, or commercial assets.

## Use

Provide references with explicit roles, for example:

```text
Image 1: character identity
Image 2: outfit construction
Image 3: pose and camera
Image 4: layout reference

Character: Subaru Awa, Girls Band Cry
Copy: canon-informed; exact title required
```

For exact small text, request `production-overlay mode`. The skill will reserve type zones in the image prompt and supply editable strings with placement guidance for Photoshop, Figma, or InDesign.

## Design principles

1. Preserve identity without borrowing faces or expressions from unrelated references.
2. Extract each layout reference's own visual system; never apply a fixed house palette by default.
3. Keep the face, hands, and focal details clean; confine print texture to intentional non-focal areas.
4. Do not invent story facts from resemblance. Distinguish canon fact, creative interpretation, and decorative copy.
5. Do not reproduce individual reference artworks. Use visual principles, not copied elements.

## License

MIT. See [LICENSE](LICENSE).
