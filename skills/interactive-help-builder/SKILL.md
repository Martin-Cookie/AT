---
name: interactive-help-builder
description: "Create interactive HTML help systems and documentation for web applications. Use this skill whenever the user wants to build a help center, user guide, contextual help, tooltips, FAQ, troubleshooting guide, or any form of interactive documentation for their application. Triggers include: 'create help for my app', 'build a help center', 'make user documentation', 'interactive guide', 'onboarding wizard', 'FAQ page', 'troubleshooting guide', 'how-to documentation', or any request to create help content based on application discovery data or screenshots. Also use when the user says things like 'help my users understand the app' or 'we need documentation for our tool'."
---

# Interactive Help Builder

You are creating a polished, interactive HTML help system for a web application. The output is a self-contained HTML file (or set of files) that serves as a comprehensive help center users can browse, search, and navigate.

## Before You Start

Check if app discovery data exists in `discovery-data/`. If it does, use it as your primary source. If not, you'll need the user to provide:
- Screenshots of the application
- Description of main features and workflows
- Any existing documentation or notes

If neither discovery data nor user-provided materials are available, suggest running the **app-discovery** skill first.

## Output Format

Create a single, self-contained HTML file with embedded CSS and JavaScript. The file should work offline — no external dependencies except optional CDN imports for icons or fonts.

### Required Sections

1. **Welcome / Overview** — Brief app description, what users can find in the help
2. **Getting Started** — First-time setup, login, initial configuration
3. **Feature Guides** — One section per major feature area, with:
   - What it does (purpose)
   - How to access it (navigation path)
   - Step-by-step instructions with screenshots
   - Tips and common pitfalls
4. **Workflows / How-To** — Task-oriented guides (e.g., "How to create an order")
5. **FAQ** — Common questions with expandable answers
6. **Troubleshooting** — Common problems and solutions
7. **Search** — Client-side full-text search across all help content

### Design Principles

The help system should feel professional and be genuinely useful. Here's what matters:

**Navigation that works** — Users come to help when they're stuck or frustrated. They need to find answers fast. Use a sidebar navigation with collapsible sections, breadcrumbs, and a prominent search bar. The search should work instantly (client-side) and highlight matches.

**Screenshots that teach** — Don't just dump screenshots. Annotate them — use numbered callouts, highlight the relevant button or field, add brief captions. A screenshot without context is just a picture. Consider using CSS to add subtle borders and shadows to screenshots so they stand out from the text.

**Progressive disclosure** — Start with the simple explanation, then offer "Learn more" or expandable sections for advanced details. Not everyone needs to know about every edge case, but power users should be able to find that information.

**Consistent structure** — Every feature guide should follow the same pattern so users learn how to read the help system itself:
1. What is this? (one sentence)
2. Where to find it (navigation path with breadcrumb-style formatting)
3. How to use it (numbered steps with screenshots)
4. Tips (optional, collapsible)
5. Related features (links to other relevant sections)

**Mobile-friendly** — Use responsive CSS. The sidebar should collapse into a hamburger menu on small screens.

### Technical Implementation

```html
<!DOCTYPE html>
<html lang="cs">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[App Name] — Nápověda</title>
  <!-- Embed all CSS inline -->
  <style>
    /* Use CSS custom properties for theming */
    :root {
      --primary: #2563eb;
      --primary-light: #dbeafe;
      --sidebar-width: 280px;
      --content-max-width: 800px;
    }
    /* ... rest of styles ... */
  </style>
</head>
<body>
  <nav id="sidebar"><!-- Sidebar navigation --></nav>
  <main id="content"><!-- Help content sections --></main>
  <script>
    // Client-side search, navigation, section toggling
  </script>
</body>
</html>
```

Key implementation details:
- Use `<details>` and `<summary>` for expandable FAQ items
- Implement search with a simple index built from all text content on page load
- Screenshots should be embedded as base64 or referenced as relative paths (ask user preference)
- Use `scroll-behavior: smooth` for anchor navigation
- Add `print` media query styles for users who want to print sections

### Screenshot Integration

When incorporating screenshots from discovery data:

1. **Reference format**: Use `<img src="screenshots/filename.png" alt="descriptive alt text">`
2. **Annotated screenshots**: If the original screenshots need annotations (numbered callouts, highlighted areas), create annotated versions using HTML/CSS overlays:
   ```html
   <div class="screenshot-container">
     <img src="screenshots/dashboard.png" alt="Dashboard overview">
     <div class="callout" style="top: 20%; left: 65%;">
       <span class="callout-number">1</span>
       <span class="callout-text">Click here to create a new order</span>
     </div>
   </div>
   ```
3. **Lazy loading**: Use `loading="lazy"` on images to improve initial page load

### Language

Write help content in the same language the application uses. If the app is in Czech, write help in Czech. If in English, write in English. Ask the user if unsure. Use clear, simple language — help documentation is not the place for jargon or marketing speak.

### Generating from Discovery Data

If `discovery-data/` exists, use it as follows:

- `navigation-map.json` → Help sidebar structure (mirror the app's own navigation)
- `screens.json` → Individual feature guide pages (one per screen or logical group)
- `workflows.json` → How-To / Workflow guides (one per workflow)
- `discovery-log.md` → FAQ items (turn observations and pain points into Q&A)
- `screenshots/` → Embedded images in guides

The help structure should roughly mirror the application's own navigation — when a user is on the "Orders" page and opens help, they should be able to find the "Orders" section easily.

## Quality Checklist

Before delivering the help file:

- [ ] Every section in the sidebar actually links to content (no dead links)
- [ ] Search works and returns relevant results
- [ ] All screenshots load correctly
- [ ] The page is responsive (test by resizing browser)
- [ ] FAQ answers are actually helpful (not just restating the question)
- [ ] Workflows have clear numbered steps
- [ ] Navigation breadcrumbs are accurate
- [ ] No placeholder text remains (like "Lorem ipsum" or "TODO")

## Iteration

After the first version, ask the user to review and provide feedback. Common improvement areas:
- Missing features or workflows
- Inaccurate descriptions (the user knows their app better than you do)
- Tone adjustments (too formal? too casual?)
- Additional FAQ items based on real user questions
- Accessibility improvements
