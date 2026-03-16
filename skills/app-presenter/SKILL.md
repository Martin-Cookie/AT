---
name: app-presenter
description: "Create interactive HTML presentations and walkthroughs showcasing web application features. Use this skill whenever the user wants to create a presentation, demo, walkthrough, showcase, or tour of their application's functionality. Triggers include: 'create a presentation of the app', 'make a demo walkthrough', 'showcase the features', 'interactive tour', 'onboarding presentation', 'feature overview', 'app demo', or any request to present an application's capabilities in an engaging, visual, interactive format. Also use when the user says 'show what the app can do' or 'present the main features to stakeholders'. This produces HTML presentations, not PowerPoint — for .pptx files, use the pptx skill instead."
---

# App Presenter

You are creating an interactive, visually engaging HTML presentation that showcases a web application's main features and workflows. Think of it as a guided tour someone can click through at their own pace — with real screenshots, smooth transitions, and clear explanations.

## Before You Start

Check if app discovery data exists in `discovery-data/`. If it does, use it as your primary source. If not, you'll need the user to provide screenshots and feature descriptions.

Ask the user about:
- **Audience** — Is this for new users (onboarding), stakeholders (selling the app), or internal team (training)?
- **Scope** — All features or specific subset?
- **Tone** — Formal/corporate or casual/friendly?
- **Language** — Czech, English, or other?

## Output Format

A single self-contained HTML file that functions as a slide-based interactive presentation. It should work offline and look polished enough for a stakeholder demo.

### Presentation Structure

1. **Title Slide** — App name, subtitle, company logo (if provided)
2. **Overview Slide** — What the app does, who it's for, key value propositions (3-5 bullet points max)
3. **Feature Slides** — One slide (or slide group) per major feature:
   - Feature name and one-line description
   - Screenshot showing the feature
   - 3-4 key capabilities highlighted with icons or callouts
   - Optional: animated callouts that appear in sequence
4. **Workflow Demo Slides** — Walk through 2-3 key workflows step by step:
   - Each step gets its own sub-slide with screenshot and description
   - Progress indicator showing where in the workflow the viewer is
5. **Summary Slide** — Key takeaways, benefits recap
6. **Call to Action** — What should the viewer do next? (Start using the app, contact someone, etc.)

### Design System

Use a modern, clean design. Here's the visual language:

```css
:root {
  /* Primary palette — adjust to match the app's branding if known */
  --primary: #2563eb;
  --primary-dark: #1d4ed8;
  --primary-light: #eff6ff;
  --accent: #f59e0b;

  /* Layout */
  --slide-max-width: 1200px;
  --slide-padding: 60px;

  /* Typography */
  --font-heading: 'Inter', -apple-system, sans-serif;
  --font-body: 'Inter', -apple-system, sans-serif;
  --heading-size: 2.5rem;
  --body-size: 1.1rem;
}
```

Design principles:
- **One idea per slide** — Don't cram everything in. Let each feature breathe.
- **Screenshots are the star** — Make them large and prominent. Text supports the visual, not the other way around.
- **Consistent layout** — Use 2-3 slide layouts and stick to them (title slide, feature slide with left text / right image, full-width screenshot with overlay text)
- **Subtle animations** — Fade-in for text elements, slight scale for screenshots on entry. Nothing flashy — keep it professional.
- **Dark/light options** — Consider offering a toggle or at least designing for projection-friendly contrast.

### Navigation & Interaction

The presentation needs smooth, intuitive navigation:

- **Arrow keys** (left/right) to navigate between slides
- **Click navigation** — Previous/Next buttons, plus clickable slide indicators (dots or thumbnails)
- **Progress bar** at the top or bottom showing position
- **Keyboard shortcut 'F'** for fullscreen mode
- **Touch support** for tablet/phone viewing (swipe left/right)
- **Slide counter** — "3 / 12" indicator
- **Optional: Table of contents** — Accessible via menu button, lets viewers jump to specific sections

### Slide Transitions

Use CSS transitions, not JavaScript animation libraries. Keep it simple and performant:

```css
.slide {
  opacity: 0;
  transform: translateX(30px);
  transition: opacity 0.4s ease, transform 0.4s ease;
}
.slide.active {
  opacity: 1;
  transform: translateX(0);
}
```

### Screenshot Treatment

Screenshots should look polished:
- Add a subtle shadow and rounded corners
- For browser-based apps, consider wrapping in a mock browser chrome frame
- Use CSS `object-fit: contain` to handle different aspect ratios
- Implement zoom-on-click for detailed views (lightbox-style overlay)
- Add numbered callouts to highlight specific UI elements being discussed

### Feature Highlight Patterns

For feature slides, use visual callout patterns:

**Pattern A: Split layout**
```
┌─────────────────────────────────────┐
│  Feature Name          │            │
│  Description text      │ Screenshot │
│  • Capability 1        │            │
│  • Capability 2        │            │
│  • Capability 3        │            │
└─────────────────────────────────────┘
```

**Pattern B: Full screenshot with overlay**
```
┌─────────────────────────────────────┐
│         [Full Screenshot]           │
│  ┌─────────────────────────┐        │
│  │ Feature Name             │       │
│  │ Key point about this     │       │
│  └─────────────────────────┘        │
└─────────────────────────────────────┘
```

**Pattern C: Step-by-step workflow**
```
┌─────────────────────────────────────┐
│  Workflow: Create New Order         │
│  Step 2 of 5                        │
│  ┌──────────────────────────────┐   │
│  │     [Screenshot of step]      │  │
│  └──────────────────────────────┘   │
│  Fill in customer details and       │
│  select the delivery method.        │
│  [← Previous Step] [Next Step →]    │
└─────────────────────────────────────┘
```

### Generating from Discovery Data

If `discovery-data/` exists:

- `navigation-map.json` → Presentation outline (each top-level nav item gets a feature section)
- `screens.json` → Content for feature slides (use descriptions, key elements, screenshots)
- `workflows.json` → Workflow demo slides (steps become sub-slides)
- `screenshots/` → All slide visuals

Prioritize by importance: start with the most-used features and most critical workflows. Not everything from discovery needs to make it into the presentation — a focused 15-20 slide presentation is better than a 60-slide exhaustive tour.

### Audience-Specific Adjustments

**For onboarding (new users):**
- Focus on "how to get started" workflows
- Include tips and shortcuts
- Add a "What to do next" section at the end
- Tone: friendly, encouraging

**For stakeholders (decision-makers):**
- Lead with value propositions and business impact
- Focus on capabilities, not step-by-step instructions
- Include data/metrics if available
- Tone: professional, confident

**For training (team members):**
- Detailed workflow walkthroughs
- Include edge cases and tips
- Reference the help documentation for deeper dives
- Tone: practical, thorough

## Quality Checklist

Before delivering:

- [ ] All slides have content (no placeholder text)
- [ ] Navigation works smoothly (arrows, clicks, keyboard)
- [ ] Screenshots load correctly and look sharp
- [ ] Animations are subtle and don't distract
- [ ] Presentation looks good in fullscreen
- [ ] Text is readable (sufficient contrast, appropriate size)
- [ ] Works on mobile/tablet (responsive)
- [ ] Consistent visual style throughout
- [ ] Total slide count is appropriate (15-25 for most cases)
