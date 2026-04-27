---
name: "nano-banana-2"
description: >
  Use this skill whenever the user requests image generation, visual creation, illustration, or photo editing.
  Triggers: "צור תמונה", "generate image", "make a visual", "design", "illustrate", "draw", "photo of".
  Requires the nanobanana MCP server to be running (configured in .mcp.json).
---

# Nano Banana 2 — Image Generation Skill

Nano Banana 2 is Google's Gemini 3.1 Flash Image model — fast, high-quality image generation with 4K output.
Access is via the `nanobanana` MCP server using the `generate_image` tool.

---

## When to Use

Use this skill when:
- User requests an image, illustration, photo, visual, or design
- User wants to edit or modify an existing image
- Agent יובל is building a prompt and ready to generate

---

## Generating an Image

Call the MCP tool `generate_image` with these parameters:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `prompt` | string | required | English-language image description |
| `model_tier` | string | `"nb2"` | Use `"nb2"` for Nano Banana 2 (fast + 4K) |
| `aspect_ratio` | string | `"1:1"` | Options: `"1:1"`, `"16:9"`, `"9:16"`, `"21:9"` |
| `resolution` | string | `"4k"` | Use `"4k"` for maximum quality |
| `output_path` | string | required | Always save to `outputs/<timestamp>_<slug>.png` |
| `n` | int | `1` | Number of variations (1–4) |

### Output Path Convention
```
outputs/YYYYMMDD_HHMMSS_<short-description-slug>.png
```
Example: `outputs/20260427_143022_sunset-beach-minimal.png`

---

## Prompt Engineering Guidelines

Write prompts in **English** — the model performs best with English.
Structure: `[subject], [style], [lighting], [composition], [color palette], [quality modifiers]`

**Good prompt example:**
```
A minimalist sunset over a calm beach, soft pastel colors,
golden hour lighting, wide angle composition, warm orange and pink tones,
4K, photorealistic, high detail
```

**Aspect ratio guide:**
- Square content (social media posts, avatars) → `1:1`
- Landscape / banner / hero image → `16:9`
- Portrait / story / mobile → `9:16`
- Cinema / ultra-wide → `21:9`

---

## Error Handling

| Error | Cause | Resolution |
|-------|-------|------------|
| `API key not found` | `GOOGLE_API_KEY` missing in `.mcp.json` | User must add their key to `.mcp.json` |
| `MCP server not running` | nanobanana server not started | Ensure MCP is configured and Claude Code restarted |
| `Model unavailable` | Rate limit or quota | Retry after a moment; consider `model_tier: "flash"` |

---

## Example Call

```
Tool: generate_image
Parameters:
  prompt: "Abstract geometric pattern, bold primary colors, flat design,
           clean lines, modern minimalist style, 4K"
  model_tier: "nb2"
  aspect_ratio: "1:1"
  resolution: "4k"
  output_path: "outputs/20260427_143022_abstract-geometric.png"
  n: 1
```
