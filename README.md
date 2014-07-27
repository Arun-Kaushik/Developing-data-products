
Developing-data-products
========================


#### Shiny Application

##### Solution

The Shiny application itself is within the "app" directory and can be executed by running the following command.

```
library (shiny)
runApp ("app")
```

##### Instructions

Write a shiny application with associated supporting documentation. The documentation should be thought of as whatever a user will need to get started using your application.

* Deploy the application on Rstudio's shiny server
* Share the application link by pasting it into the text box below
* Share your server.R and ui.R code on github

The application must include the following:
* Some form of input (widget: textbox, radio button, checkbox, ...)
* Some operation on the ui input in sever.R
* Some reactive output displayed as a result of server calculations
* You must also include enough documentation so that a novice user could use your application.
* The documentation should be at the Shiny website itself. Do not post to an external link.

The Shiny application in question is entirely up to you. However, if you're having trouble coming up with ideas, you could start from the simple prediction algorithm done in class and build a new algorithm on one of the R datasets packages. Please make the package simple for the end user, so that they don't need a lot of your prerequisite knowledge to evaluate your application. You should emphasize a simple project given the short time frame.  

#### Reproducible Pitch Presentation

##### Solution

The Slidy presentation is within the "presentation" directory.


The presentation can be published to Github with the following command.  Ensure that SSH access has been established to Github using these instructions; 

https://help.github.com/articles/error-permission-denied-publickey.

```
publish(user = "nickwallen", repo = "devdataprod-project")
```

##### Instructions

OK, you've made your shiny app, now it's time to make your pitch. You get 5 slides (inclusive of the title slide)  to pitch a your app. You're going to create a web page using Slidify with an html5 slide deck.

Here's what you need.
* 5 slides to pitch our idea done in Slidify
* Your presentation pushed to github
* A link to your github presentation pasted into the text box below

Your presentation must satisfy the following
* It must be done in Slidify
* It must be 5 pages
* It must be on github
* It must contained some embedded R code that gets run when slidifying the document

Notice to publish your slidify presentation to github, there's the publish command. This link outlines how to do it (it's one line). 

http://slidify.org/publish.html

You can also do it manually, though your github branch must have a .nojekyll fle and be on a branch names gh-pages. There's more on gh-pages here https://pages.github.com/ though remember the slidify publish command takes care of this for you if you'd like.


## mtcars dataset - Description

### Motor Trend Car Road Tests

> The data was extracted from the 1974 Motor Trend US magazine, and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973–74 models).

### Source
> Henderson and Velleman (1981), Building multiple regression models interactively. Biometrics, 37, 391–411.

```{r}
library(datasets)
head(mtcars, 3)
```

---

## mtcars dataset - Format

**A data frame with 32 observations on 11 variables.**

| Index | Field | Detail |
------- | ----- | ------ |
| [, 1] | mpg | Miles/(US) gallon |
| [, 2]  | cyl | Number of cylinders |
| [, 3]	| disp | Displacement (cu.in.) |
| [, 4]	| hp | Gross horsepower |
| [, 5]	| drat | Rear axle ratio |
| [, 6]	| wt | Weight (lb/1000) |
| [, 7]	| qsec | 1/4 mile time |
| [, 8]	| vs | V/S |
| [, 9]	| am | Transmission (0 = automatic, 1 = manual) |
| [,10]	| gear | Number of forward gears |
| [,11]	| carb | Number of carburetors |

---

## Analysis - main code

```r
  formulaTextPoint <- reactive({
    paste("mpg ~", "as.integer(", input$variable, ")")  })
  
  fit <- reactive({
    lm(as.formula(formulaTextPoint()), data=mpgData)  })
  ...
  output$fit <- renderPrint({
    summary(fit()) })
  
  output$mpgPlot <- renderPlot({
    with(mpgData, {
      plot(as.formula(formulaTextPoint()))
      abline(fit(), col=2)
    })  })

```
