# Prept — Todo / Ideas

Use this file to capture simple ideas and feature requests to consider adding to the app later. Each entry includes a short summary, motivation, possible implementation notes, acceptance criteria, and a suggested priority.

---

## Idea 1 — Add Pictures to recipes
- Status: Proposed
- Priority: High
- Created: 2025-10-18

Summary
- Allow users to attach one or more photos to a recipe (photo of the finished dish, step photos, or scanned recipe).

Motivation
- Improves usability and appeal — visual reference makes recipes easier to follow and encourages reuse.
- Useful when extracting recipes from photos (OCR): allow saving the source image with the parsed recipe.

Implementation ideas
- Data: extend recipe object with `images: [{ id, name, dataUrl }]` where `dataUrl` stores a Base64-encoded image (local-first).
- UI: in Add/Edit Recipe modal show image upload area with preview, remove, and reorder controls.
- Storage: persist images in localStorage together with recipes (consider size limits — warn for large files).
- Optional: create a small thumbnail when saving to reduce storage (canvas downscale).
- For AI OCR flow, attach the original image to the generated recipe record.
- Consider using the existing file inputs in the AI Image tab as a starting point.

Acceptance criteria
- Users can upload one or more images when creating or editing a recipe.
- Uploaded images show as previews in the Edit form.
- Images are saved with the recipe and re-displayed when viewing the recipe card/details.
- Users can remove images from a recipe.
- App gracefully warns if an image is too large to store in localStorage.

Notes / Risks
- localStorage has limited capacity — large images may exceed quota. Consider using compressed thumbnails or IndexedDB for larger storage.
- Keep privacy local-first: do not upload images anywhere by default.

Related files/components
- Add/Edit modal (`AddRecipeModal` in index.html)
- Recipe card and detail view in `RecipeBookView`
- AI OCR flow (`handleAIImageUpload`)

---

## Idea Template
- Status: Proposed / In Progress / Done
- Priority: Low / Medium / High
- Created: YYYY-MM-DD

Summary
- Short one-line description.

Motivation
- Why this adds value.

Implementation ideas
- Bullet list of approaches and technical notes.

Acceptance criteria
- What must be true for this to be considered complete.

Notes / Risks
- Caveats, storage, performance, or privacy concerns.

Related files/components
- List of places in the code to modify.

---

## Quick backlog (brain dump)
- Improve randomizer: prefer fresh vs repeated recipes weighting.
- Export/import recipes as JSON file (for backup/share).
- Sync with cloud (opt-in) — use OAuth + simple API (optional).
- Add recipe categories / tags and filter in selector.
- Drag-and-drop week planner to assign meals.
- Grocery list export (CSV / print-friendly).
- Recurring favorites: mark favorite recipes and prioritize them in randomizer.
- Accessibility audit: keyboard navigation & ARIA labels for modals and controls.
- Allow user specified API Key ✅

---