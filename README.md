# R Reproducibility Challenge

* [Setup](#setup)
* [Challenges](#challenges)
* [Legal](#legal)

For this challenge, imagine you have been given a small project at the start of
your lab rotation. Your first task is to reproduce the results and organize the
project files. The instructions left to you by the former postdoc are below.
What are the main challenges you face in trying to reproduce the code?

---

Email from former postdoc:

> Hi! Welcome to graduate school! I'm a former postdoc in the lab, and now I'm
super busy running my own lab. My former adviser informed me that you're looking
for a rotation project. A few years ago I started investigating if one of our
transgenic mouse lines had a growth phenotype. I measured the weight (in grams)
of 30 wild type mice and 30 transgenic mice (see weights.csv). I tested for a
difference in weight using a t-test (see t-test.Rmd), but I was worried about
the non-normality of the data (see visualization.Rmd). Thus I decided to do
permutations to assess significance (see permutations.Rmd). I got a
permutation-based p-value of 0.011. Could you start by re-running the code to
confirm you get the same result?

## Setup

1. Click [here][zip] to download the project as a zip file

1. Extract the files using `unzip` in the Terminal or using the archival
software available on your computer (e.g. Archive Utility on macOS, 7zip on
Windows). On Windows 10, right-click on the zip file and select "Extract
All...".

1. Double-click on the the file `r-reproducibility-challenge.Rproj` to open
the project in RStudio

1. Install [rmarkdown][]

    ```
    install.packages("rmarkdown")
    ```

[zip]: https://github.com/jdblischak/r-reproducibility-challenge/archive/master.zip
[rmarkdown]: https://rmarkdown.rstudio.com/

## Challenges

### 1. Run the code

Try running the code. You can use the RStudio Knit button or run `render`
directly in the R console:

```
library("rmarkdown")
render("visualize.Rmd")
```

What errors prevented the code from running? How can you fix them?

### 2. Organize the files

Create two new directories: `analysis` and `data` (use `dir.create()`, `mkdir`
in the Terminal, or the RStudio files pane). Move the R Markdown files to
`analysis` and the data file to `data` (use `file.rename()`, `mv` in the
Terminal, or the RStudio files pane). Make sure to update the file paths! Hint:
`..` is the shortcut for the directory up one. Use the RStudio Knit button or
`render()` to confirm you can run the code in each of the files after updating
the file paths.

### 3. Make it a website

Currently the results are 3 separate HTML files that are saved in the same
directory as the source R Markdown files. To improve this, make the results an
interconnected website ([documentation][]).

[documentation]: https://rmarkdown.rstudio.com/rmarkdown_websites.html

First, create a file in `analysis` called `index.Rmd`. This is the main landing
page of your website, so write a brief note about the project. Copy the template
below as a starting point. It uses [Markdown syntax][md] to create hyperlinks to
the other analyses.

[md]: https://guides.github.com/features/mastering-markdown/

```
---
title: "Home"
output: html_document
---

Are transgenic mice bigger or smaller than wild type mice? The weights of 30
wild type and 30 transgenic mice were [visualized](visualize.html) and assessed
for statistically significant differences using a [t-test](t-test.html) and via
[permutations](permutations.html).
```

Second, create a file in `analysis` called `_site.yml` to configure the website.
Save the output in the root of the project in a directory called `docs` (hint:
the path needs to be relative to the location of the `_site.yml`, so you'll need
to use `..`). Also, create links in the navigation bar to the 3 different
analyses. Copy the template below into `analysis/_site.yml`, replacing the ___
with the necessary directory or filename.

```
name: "rotation-project"
output_dir: ___
navbar:
  title: "Rotation Project"
  left:
    - text: "Home"
      href: index.html
    - text: "Visualize"
      href: ___
    - text: "t-test"
      href: ___
    - text: "Permutations"
      href: ___
```

Third, build the website using `render_site` (you can also use the RStudio Knit
button to build one file at a time):

```
library("rmarkdown")
render_site("analysis")
```

Were the files saved where you expected? Do the links in the navigation bar
work?

### 4. Make the permutation-based p-value reproducible

When you run permutations.Rmd, do you get a p-value of 0.011. Why not? How can
you improve the analysis to make the p-value reproducible? Are you able to
obtain the same result each time you re-run the code?

## Legal

The original version of this material was created and taught on 2018-04-17 as
part of the course "Responsible, rigorous and reproducible conduct of research"
at the University of Chicago.

This material is based upon work supported by the National Science Foundation
under Grant Number 1734818.

"Any opinions, findings, and conclusions or recommendations expressed in this
material are those of the author(s) and do not necessarily reflect the views of
the National Science Foundation."

All material in this repository is licensed under the
[CC0](https://creativecommons.org/publicdomain/zero/1.0/legalcode.txt) license,
which means you are free to modify and distribute without any acknowledgement.
See the file `LICENSE` for the full license text.
