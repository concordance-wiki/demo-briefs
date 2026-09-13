---
date: 2026-08-27
participants: [Participant-1, Participant-2, Participant-3, Participant-4]
decisions: [specs/decisions/publication/slots-islands-and-layers]
domain: publication
source: theme-override-model.vtt
---
# Theme override model

Working session on how a project overrides the look of its site without forking the theme, presented from a deck of six slides. Four participants: the maintainer, an author of the specifications, the integrator of the wiki and the quality owner. The deck, its PDF preview and the transcript sit next to these minutes and the build groups the four files into one page.

## What was said

- The need: an integrator wants the organisation's name, logo, colours and a label here and there, and never wants to touch the components. `theme.yaml` already carries the name, the logo, the favicon, the font families, the corner radius, the light and dark palettes, the footer and an extra stylesheet.
- The model: every page is a set of named slots, each rendered by a component with a typed view model, the contract between the generator and a theme. A theme that replaces a component keeps the view model; the accessibility checks run on the rendered pages whatever the theme, and the page budget is measured on every build.
- Islands: only the interactive parts are hydrated, the search, the mentions panel, the mode switch, one small bundle per island, loaded only by the pages that use it.
- Layers: the stylesheet of the project is loaded last, in the fourth cascade layer, so that nothing in the default theme can outrank it.
- Labels: a project overrides any message of the catalogue through `theme.yaml`, in the same syntax and with the same variables as the message it replaces; a missing variable is a configuration error that names the key.
- A type module may ship a page of its own for its type; it goes through the same slot, so the model covers the plugins too.

## Decision

Slots, islands and layers: named slots with typed view models, islands for the interactive parts only, cascade layers so that the project stylesheet wins by construction, and content that stays reachable without JavaScript. The budget stays at 150 kB per page, previews excluded.
