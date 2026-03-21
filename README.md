# Frontend Slides for OpenCode

A zero-dependency, animation-rich HTML presentation skill for [OpenCode](https://github.com/opencode-ai/opencode) — create stunning web presentations from scratch or by converting PowerPoint files.

> **Note:** This is the **OpenCode adaptation** of the original [frontend-slides Claude Code skill](https://github.com/zarazhangrui/frontend-slides). This version was created by **[@TMFNK](https://github.com/TMFNK)** and is designed for community contributions and improvements.

---

## What This Does

**Frontend Slides** helps non-designers create beautiful web presentations without knowing CSS or JavaScript. It uses a "show, don't tell" approach: instead of asking you to describe your aesthetic preferences in words, it generates visual previews and lets you pick what you like.

Here is a deck about the skill, made with the skill:

https://github.com/user-attachments/assets/ef57333e-f879-432a-afb9-180388982478

### Key Features

- **Zero Dependencies** — Single HTML files with inline CSS/JS. No npm, no build tools, no frameworks.
- **Visual Style Discovery** — Can't articulate design preferences? No problem. Pick from generated visual previews.
- **PPT Conversion** — Convert existing PowerPoint files to web, preserving all images and content.
- **Anti-AI-Slop** — Curated distinctive styles that avoid generic AI aesthetics (bye-bye, purple gradients on white).
- **Production Quality** — Accessible, responsive, well-commented code you can customize.
- **OpenCode Native** — Specifically designed for OpenCode's skill architecture.

---

## Installation

```bash
# 1. Clone this repository
git clone https://github.com/TMFNK/frontend-slides-OpenCode.git

# 2. Copy files to OpenCode skills folder
mkdir -p ~/.config/opencode/skills/frontend-slides
cp -r frontend-slides-OpenCode/* ~/.config/opencode/skills/frontend-slides/
```

That's it. The skill will be available in OpenCode.

---

## Usage

### Create a New Presentation

In OpenCode, invoke the skill and describe what you want:

```
> "I want to create a pitch deck for my AI startup"
```

The skill will:

1. Ask about your content (slides, messages, images)
2. Ask about the feeling you want (impressed? excited? calm?)
3. Generate 3 visual style previews for you to compare
4. Create the full presentation in your chosen style
5. Open it in your browser

### Convert a PowerPoint

```
> "Convert my presentation.pptx to a web slideshow"
```

The skill will:

1. Extract all text, images, and notes from your PPT
2. Show you the extracted content for confirmation
3. Let you pick a visual style
4. Generate an HTML presentation with all your original assets

---

## OpenCode Skill Configuration

This section documents the OpenCode-specific configuration differences from the original Claude Code version.

### Directory Structure

```
frontend-slides/
├── SKILL.md                 # Main skill definition (required)
├── README.md                # This file
├── STYLE_PRESETS.md         # Visual style references
├── viewport-base.css        # Mandatory responsive CSS
├── html-template.md         # HTML structure reference
├── animation-patterns.md    # Animation reference
├── LICENSE                  # MIT License
├── CONTRIBUTING.md          # Contribution guidelines
├── CODE_OF_CONDUCT.md       # Community code of conduct
└── scripts/
    └── extract-pptx.py       # PPTX extraction script
```

### SKILL.md Header

OpenCode skills require a specific YAML frontmatter in SKILL.md:

```yaml
---
name: frontend-slides
description: Create stunning, animation-rich HTML presentations from scratch or by converting PowerPoint files. Use when the user wants to build a presentation, convert a PPT/PPTX to web, or create slides for a talk/pitch. Helps non-designers discover their aesthetic through visual exploration rather than abstract choices.
license: MIT
compatibility: opencode
---
```

> **Key Difference:** The `compatibility: opencode` field indicates this version is specifically for OpenCode. The original Claude Code version uses `compatibility: claude` or similar.

> **Note:** All supporting file references in SKILL.md use bare filenames (e.g., `STYLE_PRESETS.md`) — not GitHub URLs. OpenCode reads these from the local skill directory at runtime.

---

## Included Styles

### Dark Themes

- **Bold Signal** — Confident, high-impact, vibrant card on dark
- **Electric Studio** — Clean, professional, split-panel
- **Creative Voltage** — Energetic, retro-modern, electric blue + neon
- **Dark Botanical** — Elegant, sophisticated, warm accents

### Light Themes

- **Notebook Tabs** — Editorial, organized, paper with colorful tabs
- **Pastel Geometry** — Friendly, approachable, vertical pills
- **Split Pastel** — Playful, modern, two-color vertical split
- **Vintage Editorial** — Witty, personality-driven, geometric shapes

### Specialty

- **Neon Cyber** — Futuristic, particle backgrounds, neon glow
- **Terminal Green** — Developer-focused, hacker aesthetic
- **Swiss Modern** — Minimal, Bauhaus-inspired, geometric
- **Paper & Ink** — Literary, drop caps, pull quotes

---

## Architecture

This skill uses **progressive disclosure** — the main `SKILL.md` is a concise map (~180 lines), with supporting files loaded on-demand only when needed:

| File | Purpose | Loaded When |
|------|---------|-------------|
| `SKILL.md` | Core workflow and rules | Always (skill invocation) |
| `STYLE_PRESETS.md` | 12 curated visual presets | Phase 2 (style selection) |
| `viewport-base.css` | Mandatory responsive CSS | Phase 3 (generation) |
| `html-template.md` | HTML structure and JS features | Phase 3 (generation) |
| `animation-patterns.md` | CSS/JS animation reference | Phase 3 (generation) |
| `scripts/extract-pptx.py` | PPT content extraction | Phase 4 (conversion) |

This design follows the harness engineering principle: "give the agent a map, not a 1,000-page instruction manual."

---

## Philosophy

This skill was born from the belief that:

1. **You don't need to be a designer to make beautiful things.** You just need to react to what you see.

2. **Dependencies are debt.** A single HTML file will work in 10 years. A React project from 2019? Good luck.

3. **Generic is forgettable.** Every presentation should feel custom-crafted, not template-generated.

4. **Comments are kindness.** Code should explain itself to future-you (or anyone else who opens it).

5. **Community drives excellence.** Open source adaptation enables broader contribution and improvement.

---

## Requirements

- [OpenCode](https://github.com/opencode-ai/opencode) CLI
- For PPT conversion: Python with `python-pptx` library

---

## Differences from Claude Code Version

| Aspect | Claude Code Version | OpenCode Version |
|--------|-------------------|------------------|
| Skill Location | `~/.claude/skills/` | `~/.config/opencode/skills/` |
| Compatibility Field | `claude` | `opencode` |
| Preview Directory | `.claude-design/slide-previews/` | `.opencode/slide-previews/` |

### Migration from Claude Code

If you're migrating from the Claude Code version:

1. Move files from `~/.claude/skills/frontend-slides/` to `~/.config/opencode/skills/frontend-slides/`
2. Update the `compatibility` field in `SKILL.md` from `claude` to `opencode` (or add if not present)

---

## Contributing

We welcome contributions from the community! Please see our [Contributing Guide](CONTRIBUTING.md) for details on:

- How to set up a development environment
- Code style and conventions
- How to submit pull requests
- Bug reporting and feature requests

### Quick Start for Contributors

```bash
# Fork this repository
# Clone your fork
git clone https://github.com/YOUR_USERNAME/frontend-slides-OpenCode.git

# Create a feature branch
git checkout -b feature/your-feature-name

# Make your changes
# Test locally by symlinking to your OpenCode skills directory

# Commit and push
git add .
git commit -m "Add your feature description"
git push origin feature/your-feature-name

# Open a pull request
```

---

## Credits

- **OpenCode Version:** Created by [@TMFNK](https://github.com/TMFNK)
- **Original Claude Code Skill:** Created by [@zarazhangrui](https://github.com/zarazhangrui) with Claude Code.

Inspired by the "Vibe Coding" philosophy — building beautiful things without being a traditional software engineer.

---

## License

MIT — Use it, modify it, share it. See the [LICENSE](LICENSE) file for details.

---

## Support

- **Issues:** Please report bugs and feature requests via [GitHub Issues](https://github.com/TMFNK/frontend-slides-OpenCode/issues)
- **Discussions:** Use [GitHub Discussions](https://github.com/TMFNK/frontend-slides-OpenCode/discussions) for questions and ideas
- **Contributing:** See [CONTRIBUTING.md](CONTRIBUTING.md) for how to help improve this skill
