# Rajat Vig — Computational Blog

This repository contains the source code for my personal website and computational blog, built with Quarto.

The site includes computational analyses written in Python and R. The analyses are rendered to HTML and published through GitHub Pages.

## Requirements

The project was developed and tested with:

- Quarto 1.10.18
- uv 0.12.7
- Python 3.14.7
- R 4.6.1
- renv 1.2.4

Quarto, uv, and R should be installed before setting up the project.

## Setup

Clone the repository and move into the project directory:

    git clone https://github.com/rajat-vig/rajat-vig.github.io.git
    cd rajat-vig.github.io

### Python

Python dependencies are managed with uv. The Python version is pinned in `.python-version`, and the exact dependencies are recorded in `uv.lock`.

From the project root:

    uv sync

This creates the project's Python environment in `.venv` and installs the dependencies needed to render the Python computational post.

The Python post uses the `python3` Jupyter kernel provided by the project environment. Rendering through `uv run` ensures that Quarto uses the project environment.

### R

R dependencies are managed with renv. The exact dependencies are recorded in `renv.lock`.

From the project root, restore the R environment:

    Rscript -e "renv::restore()"

The repository contains `.Rprofile` and `renv/activate.R`, which allow renv to activate the project environment when R is run from the project directory.

## Preview the website

From the project root:

    uv run quarto preview

This starts a local preview of the website.

## Render the website

From the project root:

    uv run quarto render

The rendered website is written to `docs/`.

Individual computational posts can also be rendered with:

    uv run quarto render posts/penguin-body-mass/index.qmd
    uv run quarto render posts/flipper-body-mass/index.qmd

## Reproducibility

The project uses lockfiles to record its computational dependencies:

- `uv.lock` records Python dependencies.
- `renv.lock` records R dependencies.

The Python analysis uses the `palmerpenguins` Python package, and the R analysis uses the `palmerpenguins` R package. The dataset is distributed with these packages, so the computational posts do not need to download a data file from the internet during rendering.

The data source is documented in each computational post:

- [Palmer Penguins](https://allisonhorst.github.io/palmerpenguins/)
- Palmer Station Antarctica LTER

## Build from a clean clone

To reproduce the website from scratch:

    git clone https://github.com/rajat-vig/rajat-vig.github.io.git
    cd rajat-vig.github.io

Install the Python environment:

    uv sync

Restore the R environment:

    Rscript -e "renv::restore()"

Render the complete website:

    uv run quarto render

The completed website will be in the `docs/` directory. The local rendered site can be inspected by opening `docs/index.html` in a browser, or by using:

    uv run quarto preview

No external data download is required during rendering.

## Project structure

- `posts/` — Quarto source files for computational blog posts
- `docs/` — rendered website published through GitHub Pages
- `_quarto.yml` — Quarto website configuration
- `blog.qmd` — blog listing page
- `pyproject.toml` — Python project configuration
- `uv.lock` — locked Python dependencies
- `.python-version` — pinned Python version
- `renv.lock` — locked R dependencies
- `.Rprofile` — renv project activation
- `renv/` — R environment configuration
- `.gitignore` — files excluded from Git

## Reproducibility check

The build instructions were tested from a fresh clone of this repository.
The Python environment was recreated with `uv sync`, the R environment was
restored with `renv::restore()`, and the complete website was successfully
rendered with `uv run quarto render`.
