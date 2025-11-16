# Multimodal Dataset Registry

This repository hosts a lightweight Hugo site whose single page (`layouts/index.html`) powers an interactive registry for multimodal datasets. The page provides:

- A structured intake form with required fields (type, task, modality, domain, task category, description, download links) plus retrieval-specific metadata in a collapsible section.
- A table that keeps browser-local records, supports cloning and password-gated deletion, and renders download/logistics links with rich formatting.
- Smart tagging (auto-generating tags from modality/domain/RAG info, with manual overrides) along with dropdown and text search filters for quick triage.

Legacy “personal website” content, sections, and styling assets have been removed so the repo contains only what is needed to deploy the dataset registry.

## Local Development

1. Install [Hugo Extended](https://gohugo.io/installation/) (v0.151 or later).
2. From the repo root run:
   ```bash
   hugo server -D
   ```
3. Browse to `http://localhost:1313` – the home page is rendered directly from `layouts/index.html`.

To ship a production build run `hugo`, then publish the generated `public/` directory (or let your existing GitHub Pages workflow do it automatically).

## Editing

- Update the intake/table UI in `layouts/index.html`. This single file contains the HTML, CSS, seed data, persistence logic, and filtering behavior.
- `hugo.yaml` still controls metadata such as base URL or language if you need to align with a different deployment target.
- Theme files and other Hugo directories remain in case you later expand beyond the single-page app, but no content files or static assets from the old personal site persist.

## Notes

- Entries live in `localStorage` in the user’s browser (`mmDatasetEntries-v3`); removing that key resets the registry.
- Deleting a row in the UI requires entering the password `notawesome` to avoid accidental removals.
- If you need to seed different default datasets, edit the `seedEntries` array near the bottom of `layouts/index.html`.
