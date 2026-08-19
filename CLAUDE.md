# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository overview

This is a static, dependency-free HTML/CSS/vanilla-JS project prototyping a Bangladesh education board ("Web Based Result Publication System") result-lookup portal, plus a small folder of student profile records. There is no package manager, build tool, bundler, framework, or test suite — the whole repo is meant to be opened directly in a browser or served as static files.

## Running / previewing

- No install or build step exists or is needed.
- Open `index.html` or `result-portal-template.html` directly in a browser, or serve the repo root with any static file server (e.g. `python3 -m http.server`).
- There is no linter, formatter, or test command configured for this repo.

## Structure

- `index.html` + `styles.css` — the primary demo: a phone-width card with a green government-style banner and a result-search form (Board / Examination / Year / Result Type dropdowns). It is presentational only — the form has no JS and does not actually perform a search.
- `result-portal-template.html` — a separate, fully self-contained alternative template exploring the same concept, built with Tailwind CSS (loaded from the CDN) and inline vanilla JS in a single `<script>` block. It fakes the whole flow client-side: a hardcoded `sampleData` object stands in for a real result lookup, and the "Security Code" captcha is a random 4-digit number generated and checked in the browser. There is no backend and no real data source — treat this file as UI scaffolding, not a working system.
- `students/*.md` — one Markdown file per student, containing identity fields (name, parents' names, DOB, gender, religion, address, guardian info) followed by a `## Course information` section (course/session/CGPA/passing year/college). Follow the exact section layout and field order used in `students/mst-seuli-islam.md` when adding new student records. Filenames are the kebab-case form of the student's name (e.g. `mst-seuli-islam.md`).
- `Logo.png` — the banner logo. `index.html` references it as `logo.png` (lowercase); this only resolves on case-insensitive filesystems/hosts, and will 404 as a broken image on case-sensitive static hosts. Fix the casing mismatch in one direction if touching either the image or the markup.

## GitHub workflows (`.github/workflows`)

- `label.yml` + `labeler.yml` — functional: auto-labels PRs `frontend` (`*.html/css/js`), `documentation` (`*.md`, `docs/**`), or `config` (`.github/**`, `*.yml/.yaml/.json`) based on changed paths.
- `greetings.yml`, `stale.yml`, `codeql.yml` — functional, generic community/security workflows (first-issue/PR greeting, closing stale issues/PRs, CodeQL scanning) requiring no project-specific setup.
- `google.yml`, `google-cloudrun-source.yml`, `maven-publish.yml`, and `root` (Jekyll → GitHub Pages) — leftover, unconfigured scaffolding from GitHub's workflow template gallery. They are not wired up for this project: the Maven workflow expects a `pom.xml` that doesn't exist, the Google Cloud workflows have literal `TODO` placeholders (project ID, region, cluster) and unset credentials, and the branch triggers don't match how this repo is actually used (`google.yml`/`google-cloudrun-source.yml` trigger on push to the literal branch name `"main"` — the quotes are part of the string; `root` triggers on a branch named `root`). Don't assume any of these run successfully; they need real configuration before they'd do anything.

## Conventions

- No build step for HTML/CSS/JS changes — edit files in place; there's nothing to compile.
- Commit messages are short, imperative, single-line (see `git log`).
