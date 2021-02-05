---
output: html_document
editor_options:
  chunk_output_type: console
---

# Markdown Tips and Tricks



This template comes with a few pre-configured custom elements that can be easily used to structure your markdown documents.

## Beware/ Think Boxes

These custom text boxes are adopted from [Desirée De Leon](http://desiree.rbind.io/post/2019/making-tip-boxes-with-bookdown-and-rmarkdown/) --- on her blog-post they are explained in more words and nicer pictures...

The *beware* and *think* boxes can be used by wrapping markdown text in `:::beware`/`:::think`content`:::` flags.

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

(If you are wondering what is happening under the hood: markdown will translate a `:::something`...`:::` section into `html` in the form of `<div class="something">`...`</div>`.)

## Saving and Loading Intermediate Steps

To minimize run-time when compiling my project documentation, I often pre-compute and save several intermediate steps of the scripts (eg. to a specific path - for instance  a folder called `./steps/` within the main directory).
I the load those intermediate steps during compilation (s. [3 Compilation](compilation.html) for how to compile the document).

Because of this, I want to indicate if a specific code block is not actually run by {knitr} (but their results are loaded in a hidden code block afterwards).
Those code blocks with long run-times are indicated by their slightly darker background (`executed code` vs. <span class="bg-save">`loaded code`</span>) and the *save* symbol in their upper-right corner: 

<img style="position:relative; width:40px; pointer-events:none;" src="./img/save_solid.svg">

When saving content while building a Rmarkdown script interactively, you can use *bg-save* code blocks to indicate that those blocks are not actually run.
This is how using those code blocks usually looks in my scripts:

```
`​``{r class.source="bg-save", eval = FALSE}
# run interactively one and export result, but don't run on compilation

intermendiate_step <- complicated_function(data)

saveRDS(object = intermendiate_step, 
        file = "steps/intermendiate_step.Rds")
`​``
```
```
`​``{r, include = FALSE}
# quick import on compilation
intermendiate_step <- readRDS(file = "steps/intermendiate_step.Rds")
`​``
```

The resulting output will then look like this (the second code block is hidden):


```{.r .bg-save}
# run interactively one and export result, but don't run on compilation

intermendiate_step <- complicated_function(data)

saveRDS(object = intermendiate_step, 
        file = "steps/intermendiate_step.Rds")
```

(I also use this approach if I need to load off heavy lifting tasks to a cluster but still integrating the results into the overall documentation/ project.)

:::beware
Exporting intermediate steps is convenient, yet this comes at the cost of neglecting reproducibility and is thus **dangerous** 😨!

If any part of your script upstream of the data-export changes, this will invalidate the exported files.
Remember to re-run those code-blocks in such cases.

In any case, you will want to run the scripts as a whole from start to finish **without loading intermediate steps** once your script is finalized to make sure you are not using outdated intermediate results!

You can switch the code block parameters to achieve this:

- `​{r class.source="bg-save", eval = FALSE}` $\rightarrow$ `​{r class.source="bg-save"}` 
- `​{r, include = FALSE}` $\rightarrow$ `​{r, include = FALSE, eval = FALSE}`.
:::

## Citations

It is possible to cite sources within Rmarkdown using the notion `[@sourceID1; @sourceID2]` based on the BibTex citations that are stored within the file `book.bib`.
In this {bookdown} [@Xie16] template, the References are collected in the chapter [6 References](./references.html).
You can download citations in Bibtex format (`.bib`) in basically all citation-export tools from every journal.

## More Help with Rmarkdown and Bookdown

If you want to dig deeper, have a look at the [official bookdown guide](https://bookdown.org/yihui/bookdown/), [R Markdown: The Definitive Guide](https://bookdown.org/yihui/rmarkdown/) or the [R Markdown Cookbook](https://bookdown.org/yihui/rmarkdown-cookbook/).

---
