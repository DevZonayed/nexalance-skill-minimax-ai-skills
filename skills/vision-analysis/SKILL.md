---
name: vision-analysis
description: >
  Analyze, describe, and extract information from images using the MiniMax vision MCP tool.
  Use when: user shares an image file path or URL (any message containing .jpg, .jpeg, .png,
  .gif, .webp, .bmp, or .svg file extension) or uses any of these words/phrases near an image:
  "analyze", "analyse", "describe", "explain", "understand", "look at", "review",
  "extract text", "OCR", "what is in", "what's in", "read this image", "see this image",
  "tell me about", "explain this", "interpret this", in connection with an image, screenshot,
  diagram, chart, mockup, wireframe, or photo.
  Also triggers for: UI mockup review, wireframe analysis, design critique, data extraction
  from charts, object detection, person/animal/activity identification.
  Triggers: any message with an image file extension (jpg, jpeg, png, gif, webp, bmp, svg),
  or any request to analyze/describ/understand/review/extract text from an image, screenshot,
  diagram, chart, photo, mockup, or wireframe.
license: MIT
metadata:
  version: "1.0"
  category: ai-vision
  sources:
    - MiniMax Token Plan MCP (understand_image tool)
---

# Vision Analysis

Analyze images using the MiniMax `MiniMax_understand_image` MCP tool available in the MiniMax Token Plan.

## Prerequisites

- MiniMax Token Plan subscription with valid `MINIMAX_API_KEY`
- MiniMax MCP configured in OpenCode (`MiniMax_understand_image` tool available)

## Analysis Modes

| Mode | When to use | Prompt strategy |
|---|---|---|
| `describe` | General image understanding | Ask for detailed description |
| `ocr` | Text extraction from screenshots, documents | Ask to extract all text verbatim |
| `ui-review` | UI mockups, wireframes, design files | Ask for design critique with suggestions |
| `chart-data` | Charts, graphs, data visualizations | Ask to extract data points and trends |
| `object-detect` | Identify objects, people, activities | Ask to list and locate all elements |

## Workflow

### Step 1: Auto-detect image

The skill triggers automatically when a message contains an image file path or URL with extensions:
`.jpg`, `.jpeg`, `.png`, `.gif`, `.webp`, `.bmp`, `.svg`

Extract the image path from the message.

### Step 2: Select analysis mode and call MCP tool

Use the `MiniMax_understand_image` tool with a mode-specific prompt:

**describe:**
```
Provide a detailed description of this image. Include: main subject, setting/background,
colors/style, any text visible, notable objects, and overall composition.
```

**ocr:**
```
Extract all text visible in this image verbatim. Preserve structure and formatting
(headers, lists, columns). If no text is found, say so.
```

**ui-review:**
```
You are a UI/UX design reviewer. Analyze this interface mockup or design. Provide:
(1) Strengths — what works well, (2) Issues — usability or design problems,
(3) Specific, actionable suggestions for improvement. Be constructive and detailed.
```

**chart-data:**
```
Extract all data from this chart or graph. List: chart title, axis labels, all
data points/series with values if readable, and a brief summary of the trend.
```

**object-detect:**
```
List all distinct objects, people, and activities you can identify. For each,
describe what it is and its approximate location in the image.
```

### Step 3: Present results

Return the analysis clearly. For `describe`, use readable prose. For `ocr`, preserve structure. For `ui-review`, use a structured critique format.

## Output Format Example

For describe mode:
```
## Image Description

[Detailed description of the image contents...]
```

For ocr mode:
```
## Extracted Text

[Preserved text structure from the image]
```

For ui-review mode:
```
## UI Design Review

### Strengths
- ...

### Issues
- ...

### Suggestions
- ...
```

## Notes

- Images up to 20MB supported (JPEG, PNG, GIF, WebP)
- Local file paths work if MiniMax MCP is configured with file access
- The `MiniMax_understand_image` tool is provided by the `minimax-coding-plan-mcp` package
