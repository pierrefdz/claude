---
allowed-tools: Bash(arxiv_latex_cleaner:*), Bash(pdflatex:*), Bash(bibtex:*), Bash(latexmk:*), Bash(tar:*), Bash(cp:*), Bash(mv:*), Bash(rm:*), Bash(ls:*), Bash(find:*), Bash(cat:*), Bash(mkdir:*)
description: Prepare a LaTeX project for arXiv submission
---

## Context

- Current directory: !`pwd`
- Subdirectories with .tex files: !`find . -maxdepth 2 -type d -exec sh -c 'ls {}/*.tex 2>/dev/null && echo "-> {}"' \; 2>/dev/null | grep -B1 "^->" | grep -v "^->" | head -10`
- BBL files found: !`find . -name "*.bbl" 2>/dev/null`

## Your task

Prepare a LaTeX project for arXiv submission. You should be at a **parent directory** level.

$ARGUMENTS

### Step 0: Identify the LaTeX folder (if not specified)

If the user didn't specify which folder, look for the one containing the main `.tex` file with `\documentclass`:

```bash
find . -maxdepth 2 -name "*.tex" -exec grep -l "\\documentclass" {} \;
```

Ask the user to confirm which folder to use before proceeding.

### Step 1: Clean with arxiv_latex_cleaner

```bash
arxiv_latex_cleaner path/to/my_latex/
```

This creates: `path/to/my_latex_arXiv/`

### Step 2: Copy BBL file

Find the `.bbl` file from the original compilation (if original project is not compiled, do it beforehand) and copy it into the arXiv folder:

```bash
cp path/to/my_latex/.aux/main.bbl path/to/my_latex_arXiv/
# or wherever the bbl is located
```

The BBL filename must match the main tex file (e.g., `main.tex` needs `main.bbl`).

### Step 3: Create tar.gz

```bash
cd path/to/my_latex_arXiv/
tar -czvf ../my_latex.tgz .
```

### Step 4: Test compilation

Untar in a fresh location and compile:

```bash
mkdir -p /tmp/arxiv_test && cd /tmp/arxiv_test
rm -rf * 
tar -xzvf path/to/my_latex.tgz
pdflatex -interaction=nonstopmode main.tex
pdflatex -interaction=nonstopmode main.tex
```

If errors occur, fix them in the `_arXiv` folder, recreate the tar, and test again.

### Final output

- Location of the `.tgz` file ready for upload
- Compilation status (success/errors)


$ARGUMENTS