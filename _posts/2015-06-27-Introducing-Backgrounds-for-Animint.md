---
layout: post
title: Introducting Backgrounds for Animint
date: June 27, 2015
author: Kevin
---

[Animint](https://github.com/tdhock/animint) is an R package designed to create *anim*ated and *int*eractive web graphics.  It takes a simple ggplot like this one ...


```r
library(ggplot2)
p <- qplot(wt, mpg, colour = factor(cyl), data = mtcars)
p
```

<img src="{{ site.baseurl }}/images/posts/2015-06-27-Introducing-Backgrounds-for-Animint_files/simple_ggplot-1.png" title="" alt="" style="display: block; margin: auto;" />

... and turns it into [an SVG vizualization](http://bl.ocks.org/kferris10/raw/ecfd085c1ed55b4e6715/).  The real power of animint is that, because it is a web graphic, it can be used to easily create animations or graphics with interactivity.  Checkout out [the Gallery](https://github.com/tdhock/animint/wiki/Gallery) for some examples.  To get started with animint, [check out the tutorial](https://tdhock.github.io/animint).



## Backgrounds

Last week, we were pleased to add backgrounds to animint plots.  Previously, animint plots always displayed with a blank background.

<script type="text/javascript" src="simpleanimintold/vendor/d3.v3.js"></script>
<script type="text/javascript" src="simpleanimintold/animint.js"></script><p></p>
<div id="simpleanimintold"></div>
<script>var plot = new animint("#simpleanimintold", "simpleanimintold/plot.json");</script>

With the [recent addition](https://github.com/tdhock/animint/pull/84), backgrounds, borders, and grid lines can now be included in animint plots.


```r
# devtools::install_github("tdhock/animint") ## if necessary
library(animint)
viz <- list(p = p)
# use structure() to get animint plots in a .Rmd file
structure(viz, class = "animint")
```

<p></p>
<div id="simpleanimintnew"></div>
<script>var plot = new animint("#simpleanimintnew", "simpleanimintnew/plot.json");</script>

## Custom Themes

There are many custom-built themes for ggplot2 available.  For example, `theme_bw()`


```r
p + theme_bw()
```

<img src="{{ site.baseurl }}/images/posts/2015-06-27-Introducing-Backgrounds-for-Animint_files/ggplot_theme_bw-1.png" title="" alt="" style="display: block; margin: auto;" />

Animint now supports these too!


```r
viz <- list(p = p + theme_bw())
structure(viz, class = "animint")
```

<p></p>
<div id="animintthemebw"></div>
<script>var plot = new animint("#animintthemebw", "animintthemebw/plot.json");</script>

`[ggthemr](https://github.com/cttobin/ggthemr)` and `[ggthemes](https://github.com/jrnold/ggthemes)` are two R packages that provide additional themes.  Here's the standard Highcharts theme from `ggthemes`.


```r
library(ggthemes)
p + theme_hc()
```

<img src="{{ site.baseurl }}/images/posts/2015-06-27-Introducing-Backgrounds-for-Animint_files/ggthemr_ggthemes-1.png" title="" alt="" style="display: block; margin: auto;" />

And here it is as an animint plot.


```r
viz <- list(p = p + theme_hc())
structure(viz, class = "animint")
```

<p></p>
<div id="animintggthemrggthemes"></div>
<script>var plot = new animint("#animintggthemrggthemes", "animintggthemrggthemes/plot.json");</script>

Animint handles all the `ggthemr` themes and most of the `ggthemes` (though a few [aren't working quite yet](https://github.com/tdhock/animint/issues/89)).

## World Maps

Altering the background easily makes a convincing world map.  


```r
library(maps)
countries <- map_data("world")

# plotting world map with ggplot2
p_world <- ggplot() + 
  geom_polygon(aes(x = long, y = lat, group = group), data = countries, 
               fill = "lightgrey", colour = "darkgreen") + 
  theme(panel.background = element_rect(fill = "lightblue"), 
        axis.line=element_blank(), axis.text=element_blank(), 
        axis.ticks=element_blank(), axis.title=element_blank(), 
        panel.grid.major=element_blank(), panel.grid.minor=element_blank())
structure(list(p = p_world), class = "animint")
```

<p></p>
<div id="animintmap"></div>
<script>var plot = new animint("#animintmap", "animintmap/plot.json");</script>

Check out the [pirate attacks vizualization](http://kferris10.github.io/AnimintBlog/) for a practical application.

 
