---
title       : Linear models 101! - Introduction       # Title
author      : Miguel Alba                             # Author Name
date        : 2021-10-13 19:00:00 -0400  # Date
categories  : [Statistics, Predictive Modeling] # Catagories, no more than 2
tags        : [Linear Models, Statistics, Inference, Machine learning]            # Tags, any number
pin         : false                       # Should this post be pinned?
toc         : true                        # Table of Contents?
math        : true                        # Does this post contain math?
comments    : true
# image       : /assets/img/...           # Header image path
---

# Simple Linear Regression

 We can express the behavior of several things around nature based on their relationships. There are several types of relationships between things, some of them could describe how to phenomenons are possibly linked, and some of them could be useful to understand the particular interaction between occurrences or situations. This interaction could produce most of the time outcomes or predictions.

 Predictions are based in the intuitive and mathematical relation between what is already known and what is to be estimated. If a practitioner could determinate how what is known today relates to a future event, they could use these insights to help considerably the decision making process of an institute/organization.

Francis Galton coined the term *regression*. In a famous essay, Galton posited that, despite the tendency of tall parents to produce tall children and short parents to produce short children, the average height of the children of parents of a given height tended to shift, or "regress," to the average height of the total population.

Regression analysis deals with the study of the dependence of a variable (dependent variable) on one or more variables (explanatory variables) with the objective of estimating or predicting the population mean or average value of the dependent variable.

## Linear Regression with two variables

The first step in determining whether a relationship exists between two variables is to examine the graph of the observed (or known) data. This graph, or plot, is called a scatter plot.

A scatter plot can give us two types of information. First, we can visually identify patterns that indicate that the variables are related. If this happens, we can see what kind of line, or estimating equation, describes this relationship. Second, it gives us an indication about the scale of the variables.

Using R and ggplot the an scatter plot could be visualized as follows:

```R
library(ggplot2)
ggplot(dataset,aes(first_variable, second_variable, color=categorical_variable)) + geom_point()
```

This results in the following plot for the dataset `mtcars`
![ScatterPlot2](/assets/posts/linear_models/scatter2.svg)

In this case the linear relationship is visible between Miles/(US) gallon (mpg) and Displacement (disp) segregated by the transmission (0: automatic, 1: manual), we can see that if the Miles/gallon increase the displacement of the car decreases. So there is an inverse relation between both variables.

This is linear relations sometimes are not that common in other datasets, one example in the following plot of the Corruption index vs Democracy index segregated by region (data extracted from [gapminder](https://www.gapminder.org/))

![ScatterPlot](/assets/posts/linear_models/scatter_plot.svg)

 We can see how there is no visual relation between both variables, maybe a further analysis of both variables could determine if they are at least slightly related!.


### Regression and correlation

Correlation analysis is closely related to regression analysis, although conceptually the two are very different. In correlation analysis, the main objective is to measure the strength or degree of linear association between two variables. 

Regression and correlation present fundamental differences that are worth mentioning. In regression analysis there is an asymmetry in the treatment of the dependent and explanatory variables. The dependent variable is assumed to be statistical, random or stochastic, i.e., it has a probability distribution.

### Covariance 

Covariance indicates the relationship between two quantitative variables. The covariance between the variable "x" and the variable "y" is denoted and calculated as follows:

$$conv(x,y)=\sigma_{xy}=\mathbb{E}[(X-\mu_x)(Y-\mu_y)]$$

*Population covariance

Where $mu_x$ is the population average for the variable $X$, $mu_y$ is the population average for the variable $Y$ and $\mathbb{E}$ is a expected value.

In the case of the sample covariance we have the following term:

$$conv(x,y)=\frac{\sum_{i=1}^{n}{(x_i - \bar{x})(y_i - \bar{y})}}{n}$$

where $\bar{x}$ and $\bar{y}$ correspond to the sample average for $x$ and $y$ respectively and $n$ is the number of samples 

If the covariance value is positive, it indicates that the variables are directly related, i.e. when the values of one variable increase, the values of the other variable also increase. On the other hand, if the value of the covariance is negative, it indicates that the variables are inversely related, i.e. when the values of one variable increase, those of the other decrease.

However, if the covariance between two variables is zero, it indicates that there is no linear relationship between the variables.

The covariance as a measure of the relationship between 2 variables has the following properties:
- It is invariant to changes in the origin of the two variables.
- Depends on unit changes, changing the unit of measurement of both variables changes the covariance. 
- An expression for calculating the covariance can be as follows:

    $$S_{xy}=a_{11} - \bar{x}\bar{y}$$

    Where $a_{11}$ has the following forms:
    
    $a_{11}=\frac{1}{N}\sum_{\forall i}{\sum_{\forall j}{x_i y_i n_{ij}}}$, when the observations are aggregated by frequencies

    $a_{11}=\frac{1}{N}\sum_{\forall i}{\sum_{\forall j}{x_i y_i}}$ when the observations are **NOT** aggregated by frequencies

- If the two variables are independent, their covariance is zero. 
- The covariance sees a joint comparison between two variables, if it is positive it will give us the information that at high values of one of the variables there is a greater tendency to find high values of the other variable and the other way around for low values in one of the variables. On the other hand, if the covariance is negative, the covariation of both variables will be in the opposite direction: high values will correspond to low values, and low values to high values. If the covariance is zero, there is no clear covariation in either direction. However, the fact that the covariance depends on the variables measurements does not allow comparisons to be made between one case and another.

### Correlation

The term correlation is used to denote the existence of a numerical relationship between the variables analyzed. A correlation coefficient expresses quantitatively the magnitude and direction of the relationship between two variables.

Magnitude refers to the closeness of the scatter plot data to a straight line. If the points on the graph are very close to a straight line, the correlation is said to be very strong, while if the points are far from a straight line, the correlation is weak.

Correlation is the degree of linear association between two quantitative variables. If two variables are linearly related, it indicates that a change in the value of one of them will generate a change in the other. To measure the association strength that exists between two variables the Pearson's coefficient is the most commonly used.

The direction of the linear relationship between the two variables analyzed can be of two types:

1. <u>Direct or positive relationship</u>: When as one variable increases, the other variable also increases. 
2. <u>Inverse or negative relationship</u>: When one variable increases and the other variable decreases. Example: This case occurs when analyzing the nominal value of vehicles and the years of use they have, since the more years of use a vehicle has, the lower its nominal value will be.

The correlation calculated using Pearson's coefficient estimated from the data has the following form:

$$\rho=\frac{\sigma_{xy}}{\sigma_{x}\sigma_{y}}$$

where $\sigma_{x}$ and $\sigma_{y}$ are the population variance for $x$ and $y$ respectively and  $\sigma_{xy}$ is the population covariance.

The sample Pearson's coefficient has the following form:

$$\gamma = \frac{conv(x,y)}{s_x s_y}$$

where $s_x$ and $s_y$ are the sample variances for $x$ and $y$ respectively. 

Writing the last expression in a more specific way could lead to the following term:

$$r_{xy}=\frac{\sum_{i=1}^{n}{w_i(x_i-\bar{x})(y_i-\bar{y})}}{S_X S_Y (\sum{w_i} - 1)}$$

where:

- $w_i$ represents expansion factors for each data pair $(x_i, y_i)$  (The expansion factor is a weight that is applied to each study unit in the sample to obtain a population estimate)
- $S_X$ and $S_Y$ are the standard deviations of both variables.


The correlation coefficient has the following properties:

- $r_{xy}$ is always between -1 and 1.
- $r_{xy}$ is positive when there is a positive relationship between both variables.
- $r_{xy}$ is negative when there is an inverse relationship between both variables.
- $r_{xy}$ is close to zero when there is no linear relation between both variables.

By viewing a scatter plot and calculating the correlation coefficient, the following aspects can be determined:

- If the coefficient is very close to 1, it is because the points are very close to a straight line with a positive slope. When the coefficient approaches -1, the scatter plot will show the data decaying in an inverse or negative effect (Like in the `mtcars` example above).

- If the coefficient is closer to zero it is because the points clustered around the line are not close to it (they are more random), there is no relationship between the variables.

- If the coefficient is closer to zero and the scatter plot shows strange shapes, this indicates a clear nonlinear behavior between the variables and it is necessary to use other types of measures to obtain this relationship or transformations in the models.

In R we can compute the correlation between a group of variables using `cor(data)`, for the `mtcars` example the correlation between `mpg` and `disp` is -0.84755, this is a final indication that both variables have an inverse relation.

### Regression Analysis

If the dependence of a variable with respect to a single explanatory variable is studied, such a study is considered as a **simple regression analysis**, or **two-variable regression analysis**. However, if the dependence of a variable is studied with respect to more than one explanatory variable, it is called a **multiple regression analysis**. In other words, in a **two-variable regression analysis** there is only one explanatory variable, while in a multiple regression analysis there is more than one explanatory variable.

At first glance we can see from a scatter plot if indeed two variables are related, as a result, we can draw, or "fit" a straight line through our scatter plot to represent the relationship.

When a line is drawn through the points of a scatter plot we are able to identify the degree of association between the variables. The line drawn through the points represents a direct relationship, because Y increases as X increases. If the points are relatively close to this line, we can say that there is a high degree of association between the variable X and the variable Y. 

For using and calculating simple linear regression models, the following aspects should be taken into account:

- Variable Y is known as the *response/dependent* variable, this is the variable of interest that was chosen. 
- Variable X is known as the *explanatory/independent* variable and this is the one that will attempt to have a direct relationship with the *response/dependent* variable.

- Both the *response/dependent* variable $Y$ and the *explanatory/independent* variable $X$ need to be highly correlated in order to expect a good scatter plot showing the linear relationship, if this does not occur there is probably another type of non-linear dependencies not considered by the proposed model. 

- In **Machine Learning** a synonym for these two variables are `target` (dependent variable) and `feature` (independent variable)

The relationship between variables $X$ and $Y$ can also take the form of a curve. Statisticians call it a curvilinear relationship.

To understand regression models we must go to the simplest step in which there is a possible relationship between two quantitative variables, by painting in a scatter plot the variable $X$ and $Y$ we can fit a line that represents the behavior of the data under a slope and an intercept, this line is known as **Simple Linear Regression** Line and is written as follows:

$$y=\beta x + \varepsilon$$

Where $y$ is the dependent variable, $x$ the independent variable, $\beta$ its associated slope or parameter and $\varepsilon$ the errors of the model which allow to evidence the exactitude with which the model fits the data.

A model can also be expressed as a *predictive function* as follows:

$$y=f(x_i)$$

Where $f$ is intended to show that the variable $y$ is a function of the variable $x$. 

After considering all this, some questions arise: *How can the beta parameter be estimated?* For this it is necessary to understand that the proposed model is considered as a model **without intercept**; this means that when drawing the regression line through the scatter diagram the beginning of the line will be at the coordinate (0,0) of the Cartesian plane. 

In general cases, models with intercept are more commonly used since the behavior of the data does not always follow a straight line pattern starting at the origin, for the case in which it is necessary to draw a regression line with intercept, the following model can be used:

$$y=\beta_0 + \beta_1 x + \varepsilon$$

The most common way to calculate the parameter of the simple linear regression is the **least squares method**.

$y=\beta_0 + \beta_1 x + \varepsilon$ is the model that perfectly fits the population, something that in practice is impossible (we have samples not all data). Thus, this model could be written in terms of expected values such as $\mathbb{E}[Y\| X_i] = f(x_i)$ or $\mathbb{E}[Y \| X_i] = \beta_0 + \beta_1 x_i$, so we use the following model known as *(sample regression function)* with similar notation to show what we want to estimate:

$$\hat{y}=\hat{\beta}_0 + \hat{\beta}_1 x + \hat{\varepsilon}$$

In terms of matrix notation, this expression can be seen as follows:

$$\begin{bmatrix}
y_{1}\\
\vdots \\
y_{n}
\end{bmatrix} =\begin{bmatrix}
1 & x_{11}\\
\vdots  & \vdots \\
1 & x_{1n}
\end{bmatrix}\begin{bmatrix}
\beta _{0}\\
\beta _{1}
\end{bmatrix} +\begin{bmatrix}
\varepsilon _{1}\\
\vdots \\
\varepsilon _{n}
\end{bmatrix}$$

We use the symbol "hat" (ex. $\hat{y}$) to represent the individual values of the estimated points, i.e., those points that are on the estimation line.

#### Variables linearity

linearity refers to the point at which the conditional expectation of $Y$ is a linear function of $X_i$ in a population model. Geometrically, the regression curve in this case is a straight line. In this interpretation, a regression function such as $\mathbb{E}[Y \| X_i] = \beta_0 + \beta_1 x^2_i$ is not a linear function because the variable $x$ is squared.

## Parameter estimation