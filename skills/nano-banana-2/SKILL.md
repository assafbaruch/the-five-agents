---
name: nano-banana-2
description: Generate images using Google Gemini 2.5 Flash Image API via the nano-banana MCP server. Use when the user asks to create, generate, or produce an image or visual. Also triggered when an agent needs to generate an image based on a text prompt.
---

# nano-banana-2

## When to use

Invoke this skill whenever a task requires generating a new image from a text description — whether requested directly by the user or delegated by another agent (e.g. Yuval).

## MCP Server

- **Server name:** `nano-banana`
- **Package:** `nano-banana-mcp` (via npx)
- **Env var required:** `GEMINI_API_KEY`
- **Config:** `.claude/settings.local.json`

## Available MCP Tools

| Tool | Purpose |
|------|---------|
| `generate_image` | Create a new image from a text prompt |
| `edit_image` | Modify an existing image file |
| `continue_editing` | Refine the last generated/edited image |
| `get_last_image_info` | Get metadata of the last image |
| `get_configuration_status` | Verify the API key is configured |

## How to generate an image

1. **Call** `generate_image` with:
   - `prompt` (string, required) — full image description

2. The tool saves the file automatically to:
   - Windows: `%USERPROFILE%\Documents\nano-banana-images\generated-[timestamp]-[id].png`

3. **Move** the generated file to `outputs/` and rename using the convention:
   ```
   outputs/YYYYMMDD_HHMMSS_<slug>.png
   ```

## How to edit an existing image

Call `edit_image` with:
- `prompt` (string) — what to change
- `image_path` (string) — path to the existing image

## Prompt guidelines

- Include: subject, style, lighting, color palette, mood, composition
- Be specific: "warm golden-hour lighting" beats "nice lighting"
- Write in English for best results
- Avoid prohibited content (violence, explicit material, real people)

## Error handling

| Situation | Action |
|-----------|--------|
| MCP server unavailable | Run `get_configuration_status` to diagnose; check that `GEMINI_API_KEY` is set in `.env` |
| Generation failed | Report the error and suggest rephrasing the prompt |
| API key missing | Remind user to set `GEMINI_API_KEY` in `.env` |
