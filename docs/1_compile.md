---
output: html_document
editor_options:
  chunk_output_type: console
---

# Compilation



To compile the the entire document, the {bookdown} package is used.
Unfortunately, the `Rmd` files (in fact the entire {bookdown} project) is located within a sub-folder and not in the main folder of the repositories R-project (where the `.Rproj` file is located).

As you will see, this introduces mild inconveniences --- yet this is intentional:

I often use standalone `R` scripts to explore or test ideas (to *sketch out stuff*) or I include standalone scripts that are run from the command-line (eg. something like `Rscript --vanilla R/script_xyz.R`).
I found it to be cleanest if *all* my `R` code assumes the base directory of the repository as working directory (this also has the added benefit that code from the `Rmd` scripts is executable in interactive sessions).
Yet, to avoid unnecessary clutter in the base directory, the bookdown project is collected within the `./vignettes` sub-folder.

So, for this to work, two things need to be set: 
Firstly, each `Rmd` script needs to point to it's parent directory (the base directory) at the start --- this is what the `knitr::opts_knit$set(root.dir = '../')` in every first code block does (don't run that code block interactively).

Secondly (the inconvenient part), for the *compilation* of the bookdown document we need to switch into the `./vignettes` folder:


```r
setwd("vignettes")                   # enter vignettes sub-folder
bookdown::render_book("index.Rmd")   # compile
setwd("..")                          # return to base directory
```

While this approach might seem a little tortuous, it allows for an interactive development of the individual `.Rmd` scripts during the development phase, that do not need to be adjusted to compile a consecutive project.

:::beware
Depending on the complexity of your `Rmd` scripts, running `bookdown::render_book("index.Rmd")` might take a while.
If you just want to check the current script/ chapter you can use the *Knit* button in Rstudio.
:::

---
