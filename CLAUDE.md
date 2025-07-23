# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based GitHub Pages site using the "Just the Docs" theme for Hoooon22's personal technical blog and documentation site. The site contains studies, projects, coding challenges, and TIL (Today I Learned) entries, primarily in Korean.

## Development Commands

### Local Development
```bash
# Start local development server with live reload
bundle exec jekyll serve --livereload

# Alternative commands
bundle exec jekyll serve      # Without live reload
bundle exec jekyll build      # Build only
```

### Linting and Formatting
```bash
# Run all linting checks
npm run lint

# Individual linting commands
npm run lint:css              # Lint SCSS files
npm run lint:formatting       # Check code formatting

# Format code
npm run format                # Auto-format SCSS, JS, and JSON files

# Run tests (currently runs linting)
npm test
```

### Dependencies
```bash
# Install Ruby dependencies
bundle install

# Install Node.js dependencies
npm install
```

## Site Architecture

### Content Structure
The site follows Jekyll's collection-based architecture with organized content in the `docs/` directory:

- **docs/studies/**: Learning materials organized by topic (backend, AI, AWS, OOP)
- **docs/projects/**: Project documentation for various software projects (devzip, gameServer, pongdang, etc.)
- **docs/codingtest/**: Daily coding challenge solutions and syntax references
- **docs/tils/**: Daily learning entries and technical notes

### Theme Customization
Built on Just the Docs theme with extensive customizations:

- **_includes/components/**: Reusable UI components (header, footer, navigation, search)
- **_sass/**: Custom SCSS styling with theme variables and component styles
- **_layouts/**: Custom page layouts extending the base theme
- **assets/**: Static resources including images organized by project/category

### Navigation Structure
- Uses Jekyll's front matter `nav_order` for navigation hierarchy
- Collection-based routing with `has_children: true` for parent pages
- Automatic breadcrumb generation and sidebar navigation

### Key Features
- **Search**: Lunr.js-powered search with Korean language support
- **Mermaid**: Diagram support with version 9.1.6
- **Code Copying**: Built-in code block copy functionality
- **Custom Popover System**: Interactive content overlays (implemented in index.md)
- **Multi-language Support**: Primarily Korean content with English technical terms

## Content Guidelines

### Image Handling (from .cursorrules)
Always use HTML tags for image insertion rather than Markdown syntax:
```html
<img src="../../../../assets/images/카테고리/파일명.png" alt="이미지 설명">
```

- Use relative paths based on document depth
- Keep filenames short and meaningful
- Avoid spaces and special characters in filenames
- Organize images by category in `assets/images/`

### Markdown Files
- Use front matter with proper `title`, `nav_order`, and `layout` fields
- Follow Korean writing conventions for content
- Include `has_children: true` for parent collection pages
- Use `permalink` for custom URL structures

### Styling and Theme
- SCSS files use the theme's variable system in `_sass/support/_variables.scss`
- Custom styles extend rather than override theme defaults
- Component-based architecture for reusable UI elements
- Color scheme supports both light and dark modes

## File Organization Patterns

### Content Files
- Date-prefixed files for chronological content (e.g., `230711.md`, `240825.md`)
- Category-based subdirectories for logical grouping
- Consistent naming patterns within each content type

### Assets
- Images organized by project/category in `assets/images/`
- SCSS partials follow atomic design principles
- JavaScript enhancements in `_includes/js/` and `assets/js/`

## Development Notes

- Site builds automatically via GitHub Pages
- Uses Jekyll collections for content organization  
- Gemfile specifies theme and plugin dependencies
- Package.json handles CSS/JS linting and formatting
- Docker support available via docker-compose.yml
- Analytics integration with Google Analytics (G-WTK357S14E)