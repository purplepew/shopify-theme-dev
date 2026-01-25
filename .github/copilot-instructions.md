# Shopify Liquid Theme Copilot Instructions

## Core Architecture
This is a modular Shopify theme built with Liquid. Follow the directory roles strictly:
- `sections/`: Full-width page components with `{% schema %}`.
- `blocks/`: Reusable, nestable UI components with `{% schema %}`. Use `{% doc %}` if rendered statically.
- `snippets/`: Logic/fragments rendered via `{% render 'name' %}`. MUST include `{% doc %}` header.
- `templates/*.json`: Define page structure and order of sections/blocks.
- `assets/`: Global static files only (e.g., `critical.css`). Component-specific CSS/JS should stay in their respective files.

## Coding Patterns & Conventions
- **Component Styles/Scripts**: Use `{% stylesheet %}` and `{% javascript %}` tags directly inside `.liquid` files for component-scoped logic. 
- **CSS Variables**: For schema-driven styling, pass settings as CSS variables to the root element.
  Example: `<div style="--gap: {{ block.settings.gap }}px">`
- **LiquidDoc**: All snippets and statically rendered blocks must have a `{% doc %}` block describing parameters and usage.
- **Internationalization**: Use `{{ 'general.button.label' | t }}` for all user-facing strings. Keys must exist in `locales/en.default.json`.
- **Global Objects**: Use `{{ content_for_header }}` in `layout/theme.liquid` `<head>` and `{{ content_for_layout }}` in `<body>`.

## Workflows
- **Development**: Use `shopify theme dev` to preview changes.
- **Settings**: Schema in `sections/` or `blocks/` must follow Shopify's JSON schema format.
- **Blocks**: Prefer blocks for granular UI elements that merchants need to reorder or configure individually.
