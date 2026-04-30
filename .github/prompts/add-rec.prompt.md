---
mode: agent
description: Add one or more recs to data.yml from links, names, or share URLs
---
Add the rec(s) the user provides in the chat input to `data.yml`.

Follow these rules carefully:

1. **Verify every venue first.** Resolve any share URLs (e.g. `share.google/...`, `maps.app.goo.gl/...`) by following redirects with `curl -skIL` and reading the `location:` headers to extract the real place name. Do a web search or check Google Maps to confirm the place exists, is still open, and is actually in/near Nashville. Never invent a venue.

2. **Pick the right section.** Existing sections in `data.yml`: Food, Hot Chicken, Coffee, Drinks, Outdoors, Sightseeing, Neighborhoods to Walk Around, Day Trips. If none fit, ask before creating a new section (and include an `emoji`).

3. **Match the existing item shape exactly:**
   ```yaml
   - title: <Place Name>
     description: <1–3 sentences, casual conversational tone matching the rest of the file. Mention neighborhood, what makes it worth going, any practical tip (line, hours, cash only, etc.). No marketing fluff.>
     note: <optional small note, only if there's a fun aside — usually omit>
     map: https://www.google.com/maps/search/?api=1&query=<URL+encoded+name>+Nashville+TN
     lat: <decimal>
     lng: <decimal>
   ```
   - URL-encode spaces as `+` and `&` as `%26` in the map query.
   - Lat/lng to 4 decimals is fine. Use the actual venue location, not a generic neighborhood centroid.

4. **Tone:** read the existing entries in `data.yml` first and match the voice — short, lowercase-y, opinionated, no em dashes, no "nestled in" / "vibrant" / "hidden gem" cliches (unless it really is one and we'd say it).

5. **Time-sensitive details:** if a place has a closure, renovation, seasonal hours, or recent reopening, add a section-level `callout:` (see the Parthenon entry for an example). Verify dates via web search.

6. **Insert** new items at the end of the relevant section's `items:` list, preserving indentation. Do not reorder existing items.

7. After editing, summarize what you added and flag anything that needs confirmation (uncertain location, possibly closed, ambiguous share link, etc.).
