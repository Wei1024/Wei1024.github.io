# Wei1024.github.io

Source for my personal website, <https://wei1024.github.io>, built with Quarto.
It includes two computational blog posts: one in R (Gapminder) and one in Python (Palmer Penguins).

## Requirements

Install these first (versions used to build the site):

| Tool   | Version | Install                                    |
|--------|---------|--------------------------------------------|
| Quarto | 1.10.18 | <https://quarto.org/docs/get-started/>     |
| uv     | 0.12.7  | <https://docs.astral.sh/uv/>               |
| R      | 4.6.1   | <https://cran.r-project.org/>              |

You do not need to install Python or renv yourself:
`uv sync` installs Python 3.14 (pinned in `.python-version`), and renv bootstraps itself the first time R starts in this folder.

## Build the site

Run all commands in a terminal, from the top level of the repository.

```bash
# 1. Clone the repository
git clone https://github.com/Wei1024/Wei1024.github.io.git
cd Wei1024.github.io

# 2. Create the Python environment (.venv) from uv.lock
uv sync

# 3. Install the R packages from renv.lock
Rscript -e 'renv::restore(prompt = FALSE)'

# 4. Render the site
uv run quarto render
```

`uv run` makes Quarto use the project's `.venv` for the Python post.
R finds `.Rprofile` in this folder and activates renv automatically.

## View the site

The built site is written to `docs/`. Open it locally with:

```bash
open docs/index.html        # macOS; on Linux use xdg-open, on Windows use start
```

or start a local preview server with `uv run quarto preview`.

## Data

- **R post** (`posts/gapminder-r/`): [Gapminder](https://www.gapminder.org/data/) data, via the [gapminder R package](https://github.com/jennybc/gapminder). Licensed CC BY 4.0.
- **Python post** (`posts/penguins-python/`): [Palmer Penguins](https://allisonhorst.github.io/palmerpenguins/) data, via the [palmerpenguins Python package](https://pypi.org/project/palmerpenguins/). Licensed CC0.

Both datasets ship inside their packages, so no data files are committed.
The network is needed only to install packages (steps 2 and 3), not to render the site.
