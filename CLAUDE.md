# STAT 301 — Statistical Modelling for Data Science (UBC, 2026 Summer 2)

Personal coursework directory: lecture notes, slides, in-class notebooks, data, and
assignments. Not a software project — the "code" is R inside Jupyter notebooks used to
follow along with the course.

## Layout

| Directory | Contents |
|---|---|
| `admin/` | Syllabus and course logistics (`syllabus.pdf`) |
| `slides/` | Lecture slide PDFs, named `topicN_<title>_partK.pdf` |
| `in-class/` | Jupyter notebooks (`topicN-M.ipynb`), activity instructions, and `data/` |
| `in-class/data/` | Datasets for notebooks (e.g. `wage.txt`) |
| `notes/master.md` | Running personal course notes, organized by topic (see workflow below) |
| `reading-materials/`, `tutorials/`, `worksheets/` | Currently empty; populated as the course progresses |

## Environment

- **R 4.6** (system install at `/Library/Frameworks/R.framework/Versions/4.6`), macOS arm64.
- Notebooks run on an **R Jupyter kernel** in JupyterLab.
- Command-line `Rscript` shares the same library as the notebook kernel, so
  `Rscript -e 'install.packages(...)'` makes packages available to the notebook
  **after a kernel restart**.
- Core packages used: `tidyverse`, `infer`, `cowplot`, `broom`, `moderndive`.
  Install missing ones with:
  ```r
  install.packages(c("infer", "cowplot", "broom", "moderndive"))
  ```
- `moderndive` provides the course's regression/correlation helpers
  (`get_correlation()`, `get_regression_table()`, `get_regression_points()`) — these are
  **not** part of tidyverse, so `library(moderndive)` must be loaded separately.

## Conventions & gotchas

- **Working directory = where JupyterLab was launched, not where the notebook file
  lives.** Notebooks in `in-class/` use relative paths like `read.table("data/wage.txt")`,
  which only resolve if the kernel's `getwd()` is `in-class/`. If Jupyter was started from
  the repo root, use `in-class/data/wage.txt` or `setwd("in-class")` instead. Check with
  `getwd()`.
- **`wage.txt` has a header row.** Read it with `read.table("data/wage.txt", header = TRUE)` —
  otherwise the column names are pulled in as the first data row and columns become `V1..V11`.
  Columns: `education south sex experience union wage age race occupation sector marr`.
- Slides and readings are PDFs; use the Read tool's `pages` parameter to view them.

## Notes workflow (`notes/master.md`)

- Organized under `# Topic N:` headings that track the lecture topics.
- Each topic may include a `### Questions:` subsection capturing open conceptual questions
  to resolve (e.g. "Why is the residual different than the error term?"). When answering
  such questions, consider recording the resolution back in this file.

## Topics covered so far

- **Topic 1: Simple Linear Regression** — least squares, residuals vs. error term,
  association vs. causation. Slides `topic1_..._part1/2.pdf`; notebook `in-class/topic1-1.ipynb`.
