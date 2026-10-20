# Automations (machine-readable workflows)

Files in this folder are executable workflows created by the floThink Workflow
Builder. Each carries a `type: maxos-workflow` frontmatter marker; the harness
lists, schedules, and runs them by that marker — not by this folder.

- Prefer editing workflows in the Workflow Builder. The frontmatter holds the
  recipe; the Markdown body is a human description and is safe to edit.
- Authoring one by hand is supported: read `WORKFLOW-PRIMITIVES.md` in this
  folder first. The harness regenerates that reference from the running floThink
  version, so it is always the current list of node types, fields, and library
  categories.
- Run artifacts are written to `AUTOMATE/Workflows/Automations/artifacts/`.
- Final leaf outputs are also delivered to the workspace inbox by the harness.
- Free-form workflows without the marker (e.g. in the `AUTOMATE/Workflows/` root) are
  ignored by the harness and left untouched.
- Document inputs should be selected through the Workflow Builder document
  picker. They must point to files the owner can access in the workspace or in a
  scoped organization project.

## Curated starter pack

This repository seeds exactly two executable workflows:

- [[Agent Inbox Housekeeping]] — organize inbox originals and create linked notes.
- [[Company Research Custom Prompt]] — research a company and answer a final prompt you supply.

Choose your own AI connections and models before running either workflow. A
clone does not activate schedules. The recipes are editable personal copies;
their catalogue IDs let the hosted floThink Library recognize an installed copy.

The hosted curated library is shipped separately with the application. Updating
this GitHub repository alone does not update that library. Publishing a curated
workflow requires matching application and starter-repository releases, privacy
review, and evidence of useful real results. Repository history retains retired
examples; they are no longer part of the executable starter pack.

Workflow subscriptions and in-app promotion are not available yet. Existing
workspace template updates use a preview/consent flow and preserve custom edits.
