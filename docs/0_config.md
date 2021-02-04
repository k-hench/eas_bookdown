---
output: html_document
editor_options:
  chunk_output_type: console
---

# Configuration



These are the parts of the template that you will want to adjust so that the document actually represents your own content.

## Important files

You will *definitively* need to adjust the following files before starting:

- `vignettes/_bookdown.yml`:
- `vignettes/_output.yml`
- `vignettes/index.Rmd`

### Configuration within `_bookdown.yml`

Here, you adjust the Rmd files that are collectively rendered into the bookdown document.
Update the entry `rmd_files:` to add more/ change Rmarkdown files.

```yml
rmd_files: ["index.Rmd", "0_config.Rmd", "1_compile.Rmd", "2_md_tips.Rmd", "3_template_script.Rmd", "Z_refs.Rmd"]
```

$\rightarrow$ kick out what you don't want and add new files if needed (exceptions: don't kick out `index.Rmd` and `Z_refs.Rmd`).

Other parameters that need configuration are `book_filename:` and `repo:` (unfortunately, some things need to be updated at several places: here *and* in the other important files 🙄).

This is not really important, but the naming of the bookdown file (in this case `eas_template.rds`) should probably reflect the project rater than this template.

```yml
book_filename: "eas_template"

```

You probably don't need a reference to this template in your project.

```yml
repo: https://github.com/k-hench/eas_bookdown
```

### Configuration within `_output.yml`

This is the file that mainly creates the TOC on the left hand side of the document.
Here, you can adjust the topmost entry (which is currently set to a duplication of the github repo):

```yml
toc:
  collapse: section
  before: |
    <li><a href="https://github.com/k-hench/eas_bookdown">github repository</a></li>
```

Also, you can remove or replace the MPI logo here:

```yml
after:  |
  <img style="position:absolute; bottom:0px; left:0px; width:100%; pointer-events:none;" src="./img/eas_logo.svg">
```

### Configuration within `index.Rmd`

This is where you set the information about title, author and date that will be displayed within the document.
These are set in the `yaml`-header of the document (the part at the beginning that is sandwiched by the two lines with `---`).

Things that you'll want to adjust here are:

- `title: "Ecology of Animal Societies"`
- `subtitle: "Bookdown Template"`
- `author: "Author Name"`
- `github-repo: k-hench/eas_bookdown`
- `description: "A template for Rmarkdown-based project documentation"`

## Clean Up

Before using this template for your own project, you might want to clean up content that was filled specifically for the documentation of this template.

Specifically, you might want to delete the content within the `./docs` folder to avoid carrying over compiled the documentation of this template into your own project.

Additionally you might want to remove the single entry of the bibliography file `./vignettes/book.bib` as this citation was only included for demonstration purposes and is likely to be irrelevant for your project.

## Nice-to-haves

The following are adjustments that you might *want* to customize, but you do not necessarily need to.

### Default Code Folding

This template comes with the option to toggle the folding of code blocks.
Currently, the default is set to expand the code-blocks - if you want them folded by default you can adjust by switching to `create_html_header("fold")` within the file `index.Rmd`. 

```md
`​``{r set_fold, include=FALSE}
source("R/initial_folding.R")
create_html_header("show") # either "show" or "fold"
`​``
```

### Color Scheme

If you want to change the color scheme, you can update the `css` stylesheet that is used within the bookdown project (`style.css`).
Currently the template uses two main colors that come in dark and light flavor respectively (<span class="c1l">color1 (light)</span>, <span class="c1d">color1 (dark)</span>, <span class="c2l">color2 (light)</span>, <span class="c2d">color2 (dark)</span>)

To make this a little more convenient, you can use the provided pre-cursor `scss` file (`scss` can use variables while `css` can not - so this is convenient to swap eg. colors consistently in a style-sheet).

To update the color scheme, open the `style.scss` file and adjust the color settings right at the beginning (by swapping the [hex-color codes](https://www.hexcolortool.com/#029c8c)):

```scss
$primary_color_d: #029c8c;
$primary_color_l: #6fe0d5;
$secondary_color_d: #674EA7;
$secondary_color_l: #a797cf;
$secondary_color_a: #a797cfcc;
```

To then re-compile the `css` file (which is the one that is actually used within bookdown), run the following within the *Terminal* window of Rstudio.

:::beware
The *Terminal* window is different from the *Console* window that you might be used to to run `R` interactively.
In the *Terminal* window you access the shell of your system directly. Make sure that the following is in order before you proceed:

- running `pwd` should provide the *path* of this repository (eg in my case `/path/to/eas_bookdown`)
- `scss` should be installed on your system: if you run `which scss` in the *Terminal window*, you should receive a prompt like eg. `/home/usr_name/gems/bin/scss`. If this prompts *nothing*, make sure to [install `scss` first](https://sass-lang.com/install)
:::

The actual conversion `scss` $\rightarrow$ `css`:
```sh
cd vignettes
sass --watch style.scss:style.css
```

After this, `sass` will keep running and *listen* to changes in your `css` file.
Hit `<ctrl><c>` to make it stop.

---
