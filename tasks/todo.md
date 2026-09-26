# Sunday Musings site refresh — responsive, minimalist, better UX

Goal: elevate design + UX of `index.html` while keeping the same core pieces
(title banner, search w/ suggestions, topic filter, episode cards w/ YouTube/Podcast
links, "load more", `published: false` hidden). `episodes.json` untouched.

## Plan
- [x] Drop Bootstrap, jQuery, Isotope (≈150KB of deps) → plain CSS grid + vanilla JS
- [x] Design tokens on `:root` (color, spacing, radius); light only per user (dark mode dropped)
- [x] Typography: serif display face for titles (Google Fonts), system sans for body
- [x] Header: title banner scales fluidly, short tagline + episode count
- [x] Sticky filter bar: search input (clear button, `/` shortcut) + topic select, stacks on mobile
- [x] Suggestions dropdown: keyboard navigable (↑/↓/Enter/Esc), ARIA combobox roles
- [x] Result summary line ("12 musings on *Politics*" + "Clear filters"), empty state
- [x] Cards: 16:9 image w/ fixed aspect ratio (no layout shift), episode # + date,
      title, description clamped to 4 lines with a More toggle, YouTube/Podcast as icon pills; whole
      card image links to YouTube
- [x] Responsive grid: 1 col phone → 2 → 3 → 4 on wide; 16px mobile gutters
- [x] Filtering operates on data, not DOM (re-render filtered list; "load more" still batches)
- [x] Shareable state in URL (`?topic=politics`, `?q=war`), restored on load (URL is replaced, so no back-button history)
- [x] Accessibility: focus rings, 44px touch targets, `prefers-reduced-motion`
- [x] Verify: serve locally, screenshot at 375px / 820px / 1440px, test search/filter/load-more

## Review
- User choices: go ahead, keep a styled dropdown (no chips), light theme only (dark mode dropped).
- Only `index.html` changed. Removed Bootstrap, jQuery, and Isotope; filtering now runs on the data.
- Search and topic now combine (e.g. "war" within Politics); before, each one cleared the other.
- Picking a topic from the suggestions sets the topic filter.
- Verified in headless Chrome at 375, 820, and 1440px: 1, 2, and 4 columns, no sideways scrolling, no console errors.
  Tested load more, suggestions (keyboard), search + topic together, empty state, clear, tag click, and URL restore.
- Bugs caught while checking: CSS catching the suggestion icons, header/footer losing the phone side margins,
  and the play button covering thumbnail text on touch screens (moved to the corner).
- Images (user request): all 262 JPGs resized to 800px wide, stripped of metadata, progressive, quality 80.
  `images/` went from 20MB to 11MB (~39KB average). Originals backed up in the session scratchpad.
- Follow-up (user request): cards now show date + full description + centered YouTube/Podcast only.
  Removed visible title (it's on the thumbnail; kept as image alt text), episode number, tag chips, and the More/Less clamp.
