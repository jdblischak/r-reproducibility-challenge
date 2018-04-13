# R3CR Reproducibility Challenge

2018-04-17

This excise was part of the University of Chicago course: Responsible,
rigorous and reproducible conduct of research (R3CR).

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

[zip]: https://github.com/jdblischak/r3cr-reproducibility-challenge/archive/master.zip

1. Extract the files using `unzip` in the Terminal or using the archival
software available on your computer (e.g. Archive Utility on macOS, 7zip on
Windows). On Windows 10, right-click on the zip file and select "Extract
All...".

1. Double-click on the the file `r3cr-reproducibility-challenge.Rproj` to open
the project in RStudio

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
`..` is the shortcut for the directory up one.

### 3. Make it a website

Currently the results are 3 separate HTML files that are saved in the same
directory as the source R Markdown files. To improve this, make the results an
interconnected website ([documentation][]).

[documentation]: https://rmarkdown.rstudio.com/rmarkdown_websites.html

First, create a file in `analysis` called `index.Rmd`. This is the main landing
page of your website, so write a brief note about the project.

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
you improve the analysis to make the p-value reproducible?
