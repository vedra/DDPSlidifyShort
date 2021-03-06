---
title       : My Slidify
subtitle    : Subtitle
author      : Vedrana B.
job         : 
framework   : revealjs      # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax, interactive]     # {quiz, bootstrap}
mode        : selfcontained                     # {standalone, draft}
ext_widgets : {rCharts: ["libraries/polycharts", "libraries/highcharts", 
                        "libraries/nvd3", "libraries/morris"]} 
knit        : slidify::knit2slides
---


## Predict your child's adult height

Vedrana B.

The Data Science Specialization: Developing Data Products


---

### PROJECT OVERVIEW

- Problem description: 
  
  - predict a child's adult height based on parent's heights

<p> &nbsp </p>

- Problem solution:

  - using existing Galton's dataset (1885 study)
  
      - heights of 928 children and their 205 parents (in inches)
    
      - parents represented by midparent height: 
    
          $\qquad \qquad hParent = \frac{hFather + 1.08*hMother}{2}$
      
  - linear model fit on the Galton's dataset:
  
          $\qquad \qquad \qquad hChild = \alpha * hParent + \beta$
  
  - SHINY application available online

---

### GALTON Dataset preview 




```r
# Chunk of R code for plotting interactive rCharts scatterplot
library(UsingR); require(base64enc); require(rCharts)
data(galton)
options(RCHART_WIDTH = 600, RCHART_HEIGHT = 300)
knitr::opts_chunk$set(comment = NA, results = 'asis', tidy = F, message = T)

g1 <- nPlot(child ~ parent, data = galton, type = 'scatterChart')
#g1$show('inline', include_assets = TRUE)
g1$save('fig/g1.html')
cat('<iframe src="fig/g1.html" width=100%, height=600></iframe>')
```

<iframe src="fig/g1.html" width=100%, height=600></iframe>

---

### Linear prediction model (LM)

- Linear relationship between input variable (parent height) and the output (child height)


```r
# Chunk of R code for building the LM model and for predicting:
model <- lm(formula = child ~ parent, data = galton2)
p     <- (as.numeric(input$hF) + 1.08*as.numeric(input$hM))/2
c     <- predict(model, data.frame(parent = p))
```



```r
# Chunk of R code for ploting the linear fit to the Galton data (inches):
library(ggplot2)
limits <- c(min(galton)-1,max(galton)+1)
ggplot(data = galton, aes(x=parent,y=child)) + 
    geom_point(color = "red", alpha=0.2, size=3) + geom_smooth(method='lm')  +
    labs(x = "Parent\'s height", y = "Child\'s height", title ="LM prediction using Galton\'s dataset") + 
    coord_cartesian(xlim = limits, ylim = limits) + guides(color = FALSE, fill = FALSE)
```

![plot of chunk plot2](assets/fig/plot2-1.png) 

---

### Interactive SHINY web app


- Available at: http://vedra.shinyapps.io/PAshiny/

- App source code: https://github.com/vedra/ShinyApp


<img width="340" height="210" src="AppShot.png">


### REFERENCES

- Materials on LMP, Shiny, Slidify etc: www.coursera.com

- Data info: http://www.math.uah.edu/stat/data/Galton.html

- Image source: www.pixshark.com

- Full slidify: https://vedra.github.io/DDPSlidifyFull/index.html

---
