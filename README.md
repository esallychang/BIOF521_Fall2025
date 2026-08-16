# BIOF521 Course Materials

This repository contains the practical/tutorial materials for **BIOF521**. It is set up using the **Carpentries lesson template**, which uses Markdown + Jekyll to turn the repository into a GitHub Pages website.

The main thing to know is that **most course content lives in `_episodes/`**. Instructors generally should not need to modify the underlying website template.

## Repository structure

The most useful folders/files for instructors are:

```text
BIOF521_Fall2025/
│
├── _episodes/       # Main tutorial/lesson pages
├── fig/             # Figures, screenshots and other files used in tutorials
├── data/            # Small datasets and example input/output files
├── files/           # Other downloadable supporting files
├── _extras/         # Additional pages/resources
│
├── index.md         # Homepage for the lesson website
├── setup.md         # Setup/instructions page
├── reference.md     # Reference page
├── _config.yml      # Jekyll/Carpentries site configuration
│
├── _layouts/        # Website layout files — normally do not edit
├── _includes/       # Reusable website components — normally do not edit
├── assets/          # CSS/JS and template assets
├── bin/             # Scripts used to build/check the site
└── Makefile         # Commands used to build and validate the site
```

There are also several files inherited from the Carpentries template (`CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, etc.) that are not normally relevant when updating the course.

## Editing the tutorials

The individual practicals are Markdown files in:

```text
_episodes/
```

For example:

```text
01-Week2-Loading-SRA-Data.md
02-ReadMapping_Tutorial.md
03-VariantCalling_Tutorial.md
...
```

The filenames are important because **the pages are sorted alphabetically to create the order of the lesson website**. Therefore, keep the numeric prefixes when adding or reorganising tutorials.

Each tutorial begins with YAML metadata/front matter containing information such as the page title, objectives and key points, followed by normal Markdown content. For example:

```yaml
---
title: "Hands-On: Loading Our Input Dataset Onto Galaxy"
objectives:
  - Locate a sequencing dataset...
  - Download sequencing metadata...
keypoints:
  - Data can be found on NCBI...
---
```

The files also use some Carpentries-specific Markdown formatting for things such as exercises, solutions, callouts and prerequisites. It is easiest to copy the formatting from an existing tutorial when adding a new section.

## Figures and other course files

Most screenshots and figures used in the practicals are stored in:

```text
fig/
```

This folder contains the Galaxy screenshots, plots, diagrams and other images used throughout the tutorials.

Small datasets and example outputs are generally stored in:

```text
data/
```

For example, this currently includes sample information, SRA metadata and example limma/voom results.

When adding new material, try to keep teaching data in `data/` and figures/screenshots in `fig/` rather than placing files alongside the Markdown tutorials.

## How the GitHub Pages website works

The repository is currently organised around the `gh-pages` branch.

The Markdown files themselves are **not separate hand-written HTML pages**. Jekyll reads the Markdown, `_config.yml`, layouts and includes and turns them into the website.

In `_config.yml`, `_episodes` is defined as a Jekyll collection and each episode is rendered using the Carpentries `episode` layout.

Roughly, the process is:

```text
_episode Markdown files
        ↓
Carpentries/Jekyll templates
        ↓
generated HTML pages
        ↓
GitHub Pages website
```

So for most changes, you only need to:

1. Edit the relevant `.md` file in `_episodes/`.
2. Add/update any associated files in `fig/` or `data/`.
3. Commit and push the changes.
4. Check the GitHub Pages website once the build has completed.

There is a GitHub Actions workflow in:

```text
.github/workflows/website.yml
```

which runs when changes are pushed to `gh-pages` or `main`. Among other checks, it runs:

```bash
make site
```

to make sure that Jekyll can successfully build the website.

If a commit causes a build error, **GitHub → Actions → Website** is therefore a useful first place to look.

## Previewing the site locally

This is optional — for small Markdown edits it is usually easiest simply to push the change and check GitHub Pages.

If you do want to build the site locally, the Makefile provides:

```bash
make serve
```

which builds the site and starts a local Jekyll server, or:

```bash
make site
```

which builds the website without starting the server. The generated website is placed in `_site/`.

There is also:

```bash
make lesson-check-all
```

which runs the Carpentries lesson-format checks.

Running the site locally requires the Ruby/Jekyll dependencies used by the Carpentries template, so it is not necessary unless you are making larger structural changes.

## Things you probably should **not** edit

Unless you are deliberately changing how the website looks or behaves, avoid changing:

```text
_layouts/
_includes/
assets/
bin/
Makefile
.github/workflows/
```

These are mostly inherited from the Carpentries template and control how the lesson is rendered rather than the course content itself.

Similarly, `_config.yml` controls site-wide behaviour and normally only needs changing if the course/site configuration itself is changing.

## Adding a new tutorial

The easiest approach is:

1. Copy an existing file from `_episodes/`.
2. Rename it using the next appropriate numeric prefix, e.g.

```text
10-New_Tutorial.md
```

3. Update the YAML header.
4. Replace the tutorial content.
5. Put new screenshots in `fig/`.
6. Put small input/example datasets in `data/`.
7. Commit and push.
8. Check the GitHub Pages site and the GitHub Actions build.

## In short

If you are taking over teaching the course, the main places you will probably use are:

```text
_episodes/   → edit the practical instructions
fig/         → screenshots and figures
data/        → teaching datasets/example results
index.md     → course website homepage
```

Everything else is mostly infrastructure that makes the Carpentries/Jekyll website work.
