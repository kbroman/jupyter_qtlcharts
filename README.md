## tests of R/qtlcharts in Jupyter

Simple examples of use of R/qtlcharts in a [Jupyter](https://jupyter.org/) notebook.

It's a bit cumbersome, but it works:

- save output of one of the R/qtlcharts functions to an object (rather
  than printing it)

- save that to a file with `saveWidget()`

- create a bit of html to load the file into an `<iframe>`
  (the [glue package](https://glue.tidyverse.org) is helpful for this)

- use `display_html()` from the [IRdisplay package](https://github.com/IRkernel/IRdisplay) to display it.

Here's an example:

```r
library(qtlcharts)
library(IRdisplay)
library(htmlwidgets)
library(glue)

data(grav)

file <- "html/iplot_demo.html"
height <- 500
width <- 700

h <- iplot(grav$pheno[,1], grav$pheno[,25],
           chartOpts=list(xlab=phenames(grav)[1], ylab=phenames(grav)[25],
                          height=height, width=width))

saveWidget(h, file, selfcontained=TRUE)
html <- glue('<iframe src="{file}" height="{height+100}px" width="{width+100}px"></iframe>')
display_html(html)
```

---

### License

Licensed under [GPL-3](https://www.r-project.org/Licenses/GPL-3).
