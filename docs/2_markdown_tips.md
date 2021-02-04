---
output: html_document
editor_options:
  chunk_output_type: console
---

# Markdown Tips and Tricks



## Beware/ Think Boxes

The *beware* and *think* boxes can be used by wrapping markdown text in `:::beware`/`:::think`content`:::` flags:

```
:::beware
This is a *beware* box demo!
:::
```

:::beware
This is a *beware* box demo!
:::

```
:::think
This is a *think* box demo!
:::
```

:::think
This is a *think* box demo!
:::

(If you are wondering what is happening under the hood: markdown will translates a `:::something`...`:::` section into `html` in the form of `<div class="something">`...`</div>`.)

## Saving and Loading Intermediate Steps

To minimize run-time when compiling my project documentation, I often pre-compute and save several intermediate steps of the scripts (eg. to a specific path - for instance  a folder called `./steps/` within the main directory).
I the load those intermediate steps during compilation (s. [3 Compilation](compilation.html) for how to compile the document).

Because of this I sometimes want to indicate that some code blocks are not actually run by {knitr} (but their results are loaded in a hidden code block afterwards).
Those code blocks with long run-times are indicated by their slightly darker background (`executed code` vs. <span class="bg-save">`loaded code`</span>) and the *save* symbol in their upper-right corner: 

<img style="position:relative; width:40px; pointer-events:none;" src="./img/save_solid.svg">

When saving content while building a Rmarkdown script interactively, you can use *bg-save* code blocks to indicate that those blocks are not actually run.
This is how using those code blocks usually looks in my scripts:

```
`​``{r class.source="bg-save", eval = FALSE}
# demo of bg-save code-block

intermendiate_step <- complicated_function(data)

saveRDS(object = intermendiate_step, 
        file = "steps/intermendiate_step.Rds")
`​``
```
```
`​``{r, include = FALSE}
# demo of normal  code-block
intermendiate_step <- readRDS(file = "steps/intermendiate_step.Rds")
`​``
```

The resulting output will then look like this (the second code block is hidden):


```{.r .bg-save}
# demo of bg-save code-block

intermendiate_step <- complicated_function(data)

saveRDS(object = intermendiate_step, 
        file = "steps/intermendiate_step.Rds")
```

## Citations

It is possible to cite sources within Rmarkdown using the notion `[@sourceID1; @sourceID2]` based on the BibTex citations that are stored within the file `book.bib`.
In this {bookdown} [@Xie16] template, the References are collected in the chapter [6 References](./references.html).
You can download citations in Bibtex format (`.bib`) in basically all citation-export tools from every journal.

## More Help with Rmarkdown and Bookdown

If you want to dig deeper, have a look at the [official bookdown guide](https://bookdown.org/yihui/bookdown/), [R Markdown: The Definitive Guide](https://bookdown.org/yihui/rmarkdown/) or the [R Markdown Cookbook](https://bookdown.org/yihui/rmarkdown-cookbook/).
