---
name: nano-banana-2
description: Generate images using Google Nano Banana 2 via MCP. Use when the user asks to create, generate, or produce an image or visual. Also triggered when an agent needs to generate an image based on a text prompt. Handles prompt submission and retrieval of the generated image file.
---

# nano-banana-2

## When to use

Invoke this skill whenever a task requires generating a new image from a text description — whether requested directly by the user or delegated by another agent (e.g. Yuval).

## How to generate an image

1. **Call the MCP tool** `nano_banana_generate` with:
   - `prompt` (string, required) — full image description
   - `output_path` (string, required) — destination file path (e.g. `outputs/image.png`)
   - `width` (integer, optional) — image width in pixels, default 1024
   - `height` (integer, optional) — image height in pixels, default 1024

2. **Wait** for the tool response — it returns `{ "file_path": "...", "status": "success" | "error", "message": "..." }`

3. **Report** the saved file path to the caller.

## Prompt guidelines

- Include: subject, style, lighting, color palette, mood, composition
- Be specific: "warm golden-hour lighting" beats "nice lighting"
- Max 1000 characters
- Write in English for best results
- Avoid prohibited content (violence, explicit material, real people)

## Output path convention

Always use the `outputs/` directory unless explicitly told otherwise:
```
outputs/YYYYMMDD_HHMMSS_<short-slug>.png
```

## Error handling

| Situation | Action |
|-----------|--------|
| MCP server unavailable | Report: "nano-banana-2 MCP server is not connected. Check `.claude/settings.local.json` and ensure `NANO_BANANA_API_KEY` is set." |
| Generation failed | Report the error message from the tool response and suggest rephrasing the prompt |
| Invalid output path | Create the directory if missing, then retry |
