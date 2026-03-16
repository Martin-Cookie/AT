---
name: app-discovery
description: "Systematic web application exploration and documentation skill. Use this skill whenever the user wants to explore, map, document, or understand a web application they have access to. Triggers include: 'explore my app', 'map the application', 'document the UI', 'take screenshots of the app', 'understand how the app works', 'click through the application', or any request to systematically discover and catalog a web application's screens, navigation, workflows, or features. Also triggers when the user provides login credentials or a URL to an application and wants Claude to learn how it works. Use this even if the user just says 'look at my app' or 'check out this tool we use'."
---

# App Discovery Skill

You are systematically exploring a web application to build a comprehensive understanding of its structure, navigation, features, and workflows. This discovery data will later be used to create help documentation, presentations, and training materials.

## Why This Matters

The quality of any help system, presentation, or onboarding material depends entirely on how well you understand the application. Rushing through discovery leads to incomplete documentation that misses important features or misrepresents workflows. Take your time — thorough discovery now saves enormous effort later.

## Before You Start

1. Confirm you have browser access (Claude in Chrome / MCP browser tools)
2. Get the application URL and any credentials from the user
3. Create a working directory for this discovery session:
   ```
   discovery-data/
   ├── screenshots/        # All captured screenshots
   ├── navigation-map.json # Application structure
   ├── screens.json        # Detailed screen catalog
   ├── workflows.json      # Step-by-step process flows
   └── discovery-log.md    # Running notes and observations
   ```

## Discovery Process

### Phase 1: Orientation

Start by getting the big picture before diving into details.

1. **Load the application** — Navigate to the main URL and take a screenshot
2. **Identify the navigation structure** — Look for:
   - Main menu / sidebar / top navigation
   - Breadcrumbs
   - Tab systems
   - Footer links
3. **Map the top-level sections** — Click through each main navigation item, take a screenshot of each landing page
4. **Note the application type** — Is it a CRM, ERP, project management tool, etc.? Understanding the domain helps you anticipate what features to look for

Take a screenshot at each step. Name screenshots descriptively:
- `01-login-page.png`
- `02-dashboard-main.png`
- `03-nav-settings.png`
- `04-nav-reports.png`

### Phase 2: Screen-by-Screen Catalog

For each screen/page you discover:

1. **Take a full screenshot** (scroll down if the page is long — take multiple screenshots)
2. **Record in screens.json**:
   ```json
   {
     "id": "screen-001",
     "name": "Dashboard",
     "url_path": "/dashboard",
     "parent_section": "Main",
     "screenshot_files": ["02-dashboard-main.png"],
     "description": "Main overview showing KPIs and recent activity",
     "key_elements": [
       {"type": "chart", "label": "Monthly Revenue", "location": "top-left"},
       {"type": "table", "label": "Recent Orders", "location": "center"},
       {"type": "button", "label": "Create New Order", "location": "top-right"}
     ],
     "navigation_to": "Main menu > Dashboard",
     "connects_to": ["screen-005", "screen-012"]
   }
   ```
3. **Identify interactive elements** — buttons, forms, dropdowns, filters, tabs within the page
4. **Note any sub-navigation** — tabs, accordions, or expandable sections within the screen

### Phase 3: Workflow Discovery

This is where you trace the actual processes users perform. For each major workflow:

1. **Identify the starting point** — Where does this process begin?
2. **Walk through each step** — Click through the entire process, taking screenshots at each decision point or new screen
3. **Record in workflows.json**:
   ```json
   {
     "id": "workflow-001",
     "name": "Create New Order",
     "description": "End-to-end process for creating a customer order",
     "trigger": "Click 'Create New Order' button on Dashboard or Orders page",
     "steps": [
       {
         "step": 1,
         "screen_id": "screen-005",
         "action": "Click 'Create New Order' button",
         "screenshot": "wf01-step01-click-create.png",
         "notes": "Button is in top-right corner of Orders page"
       },
       {
         "step": 2,
         "screen_id": "screen-006",
         "action": "Fill in customer details form",
         "screenshot": "wf01-step02-customer-form.png",
         "fields": ["Customer Name", "Email", "Phone", "Address"],
         "notes": "Customer can be selected from existing or created new"
       }
     ],
     "outcome": "New order is created and appears in Orders list",
     "estimated_time": "2-5 minutes",
     "complexity": "medium"
   }
   ```
4. **Note decision points** — Where does the workflow branch? What happens if the user makes different choices?
5. **Note error states** — What happens with invalid input? Are there validation messages?

### Phase 4: Build the Navigation Map

After exploring, compile everything into `navigation-map.json`:

```json
{
  "app_name": "Application Name",
  "app_url": "https://app.example.com",
  "app_type": "ERP / CRM / etc.",
  "discovered_date": "2026-03-16",
  "structure": {
    "main_navigation": [
      {
        "label": "Dashboard",
        "screen_id": "screen-001",
        "children": []
      },
      {
        "label": "Orders",
        "screen_id": "screen-005",
        "children": [
          {"label": "All Orders", "screen_id": "screen-005a"},
          {"label": "Create Order", "screen_id": "screen-006"},
          {"label": "Order Templates", "screen_id": "screen-007"}
        ]
      }
    ]
  },
  "total_screens": 24,
  "total_workflows": 8,
  "key_features": [
    "Order management",
    "Customer database",
    "Reporting and analytics"
  ]
}
```

## Screenshot Best Practices

- Use the browser's full viewport — resize to a standard width (1280px or 1440px) for consistency
- Scroll to capture full-page content when needed
- Highlight or annotate important elements when it helps clarity
- For long pages, take overlapping screenshots so nothing is missed
- Name files with a clear prefix system: `NN-section-description.png`

## Discovery Log

Keep a running `discovery-log.md` as you go. This captures things that don't fit neatly into the structured JSON — unexpected behaviors, UI quirks, accessibility issues, things that confused you (they'll confuse users too).

```markdown
# Discovery Log — [App Name]

## Session 1 — 2026-03-16

### Observations
- The navigation collapses on screens narrower than 1024px
- Settings page has 6 tabs but "Advanced" tab is only visible to admins
- Search function only searches by name, not by ID (users might expect ID search)

### Questions for user
- Is the "Archive" function reversible?
- Who has access to the "Admin Settings" section?

### Potential pain points
- The order creation form is 3 pages long with no save-as-draft
- Error messages appear at the top of the page, not next to the field
```

## Output Checklist

Before finishing discovery, verify you have:

- [ ] Screenshots of every major screen (minimum: every top-level nav item)
- [ ] `navigation-map.json` with complete app structure
- [ ] `screens.json` with all discovered screens cataloged
- [ ] `workflows.json` with at least the 3-5 most important workflows
- [ ] `discovery-log.md` with observations and notes
- [ ] Confirmed with user that no major sections were missed

## Tips

- If you encounter modal dialogs or popups, capture those too — they're often missed in documentation
- Pay attention to empty states (what does a page look like with no data?)
- Look for settings/configuration pages — these often reveal features that aren't obvious elsewhere
- Check if there are different user roles with different views
- If the app has notifications or alerts, capture examples of those
- Look for keyboard shortcuts or power-user features

## Handing Off to Other Skills

The discovery data you create here is designed to be consumed by:
- **interactive-help-builder** — to generate contextual help documentation
- **app-presenter** — to create feature presentations and walkthroughs

Save all output to the `discovery-data/` directory. Those skills will look for data there.
