# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Mintlify documentation site**. Mintlify is a modern documentation framework that uses MDX (Markdown + JSX) for content and a `docs.json` file for configuration.

## Development Commands

### Local Development
```bash
# Install Mintlify CLI globally (requires Node.js v19+)
npm i -g mint

# Start local development server
mint dev

# Start on custom port
mint dev --port 3333

# Update CLI to latest version
npm mint update

# Validate all links in documentation
mint broken-links
```

The local preview runs at `http://localhost:3000` and hot-reloads on file changes.

### Troubleshooting
- If dev server fails: Run `mint update` to get latest CLI version
- If page loads as 404: Ensure `docs.json` exists in current directory
- If encountering "sharp" module errors: Upgrade to Node v19+, remove CLI (`npm remove -g mint`), and reinstall
- For unknown errors: Delete `~/.mintlify` folder and run `mint dev` again

## Architecture

### Content Structure
- **MDX files** (`.mdx`): All documentation pages using Markdown + JSX components
- **docs.json**: Central configuration file defining navigation, theme, colors, and metadata
- **snippets/**: Reusable content snippets that can be embedded across pages
- **images/**: Static image assets
- **logo/**: Light and dark theme logo variants
- **api-reference/**: API documentation pages (can be auto-generated from OpenAPI specs)

### Navigation System
Navigation is entirely defined in `docs.json` under the `navigation` key:
- **tabs**: Top-level navigation tabs
- **groups**: Sections within each tab
- **pages**: Individual page slugs (without `.mdx` extension)

Page order in navigation matches array order in `docs.json`.

### Theme Configuration
All visual customization happens in `docs.json`:
- `colors`: Primary, light, and dark theme colors
- `logo`: Paths to light/dark logo variants
- `favicon`: Site favicon path
- `navbar`: Top navigation links and CTA button
- `footer`: Social media links

### Contextual Features
The `contextual.options` array in `docs.json` enables right-click context menu integrations (copy, view in ChatGPT, Claude, Cursor, VS Code, etc.).

## Key Files

- **docs.json**: Master configuration - navigation, theme, metadata
- **index.mdx**: Homepage/landing page
- **quickstart.mdx**: Getting started guide
- **development.mdx**: Local development instructions
- **essentials/**: Core documentation guides (markdown, code, images, navigation, settings, reusable-snippets)
- **ai-tools/**: AI tool integration guides (claude-code, cursor, windsurf)

## Content Guidelines

### MDX Components
Mintlify provides custom components for enhanced documentation:
- `<Card>`: Feature cards with icons and links
- `<CardGroup>`: Container for multiple cards
- `<Accordion>` / `<AccordionGroup>`: Collapsible content sections
- `<Steps>` / `<Step>`: Sequential step-by-step instructions
- `<Tip>`, `<Note>`, `<Warning>`, `<Info>`: Callout boxes
- `<Frame>`: Image containers with styling
- `<Columns>`: Multi-column layouts

### Frontmatter
Every `.mdx` file requires YAML frontmatter:
```yaml
---
title: "Page Title"
description: "Page description for SEO"
---
```

### Adding New Pages
1. Create new `.mdx` file in appropriate directory
2. Add frontmatter with title and description
3. Register page in `docs.json` navigation structure (use slug without `.mdx` extension)
4. Preview changes with `mint dev`

### Reusable Snippets
- Create snippets in `snippets/` directory
- Import with `<Snippet file="snippet-name.mdx" />`
- Useful for shared content across multiple pages

## Deployment

Changes are automatically deployed to production when pushed to the default branch (requires GitHub app installed from Mintlify dashboard).

## External Resources

- [Mintlify Documentation](https://mintlify.com/docs)
- [CLI Changelog](https://www.npmjs.com/package/mintlify?activeTab=versions)
- [Mintlify Dashboard](https://dashboard.mintlify.com)
