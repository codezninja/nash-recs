# Nashville Recs Page (nash-recs)

## What it is

A simple, static GitHub Pages site that lists our favorite Nashville spots (restaurants, bars, coffee, outdoors, neighborhoods, day trips). The content is driven by a YAML file so it's easy to update without touching any HTML.

## Repo

`codezninja/nash-recs`

## Architecture

- `data.yml` — All the content lives here. Sections, items, descriptions, notes, callouts. This is the only file you need to edit to add/remove/update spots.
- `index.html` — The template. Fetches `data.yml` at page load using js-yaml (loaded from cdnjs), parses it, and renders the page. You shouldn't need to touch this unless you want to change the design.

## How to update content

Edit `data.yml` and push. The YAML structure is:

```yaml
sections:
  - name: Section Name
    emoji: "🍽️"
    items:
      - title: Place Name
        description: Why it's great.
        note: Optional small note under the description
    callout: Optional callout box text for the whole section
```

To add a new spot, just add another item block under the right section. To add a whole new category, add a new section block.

## How it was built

1. Every single venue and location was verified via web search before being included. Nothing was made up.
2. Time sensitive details were checked:
   - Parthenon interior closed for HVAC until late June 2026
   - Radnor Lake reopened March 2 after ice storm
   - Cheekwood reopened March 7 after storm
   - Bolton's Franklin Pike location is permanently closed but Main St is open
3. Started as an SMS text draft, iterated on tone and content, then converted to a static HTML page, then split into YAML + HTML for easier editing.

## Design notes

- Fonts: DM Serif Display (headings) + Karla (body) from Google Fonts
- Warm cream/brown palette with orange accents
- Mobile responsive
- No external dependencies beyond Google Fonts and js-yaml CDN

## To enable GitHub Pages

Repo Settings > Pages > Source: Deploy from branch > `main` / `root`

## Agent prompt: `/add-rec`

There's a shared `add-rec` prompt that encodes the workflow for adding new spots to `data.yml` (resolve share links, verify the venue, match the existing YAML shape and tone, etc.). It lives in three places so it works across editors:

- pi: `.pi/prompts/add-rec.md` → invoke with `/add-rec <links or names>`
- Claude Code: `.claude/commands/add-rec.md` → invoke with `/add-rec <links or names>`
- VS Code (Copilot Chat): `.github/prompts/add-rec.prompt.md` → run via the chat prompt picker, then type the venues in the chat

If you change the workflow, update all three files (they share the same body). Examples:

```
/add-rec https://share.google/XyxsLpVQLndXlSFqs
/add-rec "Bastion" "Yolan"
/add-rec Beaman Park
```
