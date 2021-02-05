---
title: "Ecology of Animal Societies"
subtitle: "Bookdown Template"
author: "Author Name"
date: "2021-02-05"
documentclass: book
bibliography: [book.bib]
biblio-style: apalike
link-citations: yes
github-repo: k-hench/eas_bookdown
description: "A template for Rmarkdown-based project documentation"
editor_options: 
  chunk_output_type: console
---






# Intro

Hello 👋,

you are looking at a minimal {[bookdown](https://bookdown.org/)} template that can be used to document your coding projects.

The documentation of this template is broken down into several chunks:

- [1 Intro](./index.html): General intro to the project/ template (you are looking at this right now...)
- [2 Configuration](./configuration.html): Here you'll see which parts you should customize if you choose to adopt this template for your own projects.
- [3 Comilation](./compilation.html): How to actually compile the bookdown document once you have added you own content.
- [4 Markdown Tips and Tricks](./markdown-tips-and-tricks.html): This section includes an introduction into a couple of minor features that are build into this template and that go a little beyond the standard markdown elements. 
- [5 Template Script](./template-script.html): This is a blank section. Its purpose is to provide a minimal template that can be copied to add more sections.
- [6 References](./references.html): This is where all cited sources of your project will be listed.

To be able to use this in your own projects you will need to `R` as well as the {bookdown} package installed:

```r
install.packages("bookdown")
```

Note that the template also uses the (non-cran) package {[emo](https://github.com/hadley/emo)} to be able to use emojis within Rmarkdown.

To be able to do this as well, install {emo} with the {[remotes](https://remotes.r-lib.org/)} package:

```r
install.packages("remotes")
remotes::install_github("hadley/emo")
```

Feel free to adapt this template to your needs 😄.

## First Special Feature

Individual **code blocks can be collapsed and expanded** using the collapse button (this specific demo slider blow is a dummy though --- look in the next chapters for working examples...):

<div class="demoslider"><div class="demobg"><div class="demonob"></div></div></div>

In the upper right corner, there is also the option to **toggle the code collapsing globally**:  <button type="button" class="btn btn-default btn-xs dropdown-toggle">global code</button> 

Collapsing your code can really help to get an eagle-perspective on your scripts and to asses the degree of documentation as well as the flow of thoughts throughout / the logic behind your script.

---
