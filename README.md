# test-cases-for-modee
# Test cases from BRD

This repository automates **structured test case generation** whenever a **BRD** (or requirements document) is added or updated.

## What happens when you upload a BRD

1. Place the document under **`Requirements/BRD/`** (e.g. `Requirements/BRD/MyProduct-BRD-v1.docx` or `.md`).
2. Push your changes to the **default branch** (e.g. `main`).
3. **GitHub Actions** runs the pipeline: extract text (if supported) → generate **TSV + Excel (`.xlsx`)** + a short **Markdown** summary under **`Test cases/`**.
4. The workflow **commits** the generated files back to the same branch (no manual copy from a laptop).

> **Note:** Exact filenames and scripts depend on how your team configured the repo. Ask the owner or check **`.github/workflows/`** and **`scripts/`**.

## What you get

| Output | Purpose |
|--------|---------|
| **`Test cases/*.xlsx`** | Primary deliverable for QA / UAT (review in Excel) |
| **`Test cases/*.tsv`** | Easy diffs in Git, optional import elsewhere |
| **`Test cases/*.md`** | Human-readable overview, assumptions, open questions |

## Test case conventions (recommended)

- Each **Description** starts with **`Verify`** … (clear, professional acceptance wording).
- Table columns (example): `Test Case ID | Story Title | Description | Status | QA Name`
- **QA Name** default: set your team default (e.g. one owner per export).
- **Story Title**: document title + version, not only a ticket key.

## One-time GitHub setup

1. Repo → **Settings** → **Actions** → **General** → **Workflow permissions** → **Read and write** (so the workflow can commit results).
2. Confirm a workflow exists under **`.github/workflows/`** that triggers on `Requirements/BRD/**`.
3. Push a BRD change and open the **Actions** tab to verify a green run.

## Manual / Cursor workflow (if you are not using Actions)

1. Add the BRD under **`Requirements/BRD/`**.
2. In Cursor (or locally), run your project’s generate script(s), e.g. `python scripts/…py`.
3. Commit **`Test cases/`** outputs including **`.xlsx`**.

## Security

- Do **not** commit production secrets. Use **`.env`** locally (ignored by Git) for URLs, accounts, or tokens used in automation.

## Contributing

- Prefer **pull requests** for BRD updates and regenerated test packs.
- Keep BRD files **versioned** (date or semver in the filename helps traceability).

---

**Maintainers:** document your real paths, script names, and trigger branches in this README so uploaders only follow one source of truth.
