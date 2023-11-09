
\pagebreak 
\setcounter{chapter}{3}
\setcounter{section}{0}
\renewcommand{\thepage}{\arabic{page}}

# SDM with GLM and GAM (covariates)  (María y David)

Aquí David utilizará su amplio material de sus cursos para crear un capítulo donde haga una introducción a los GLM y GAM en el ámbito de los SDM e INLA. 

## Charting the Ecological Landscape with GLM and GAM 

Species Distribution Models (SDMs) have long been a cornerstone in ecological research, conservation planning, and environmental decision-making. These models, which aim to correlate the occurrence or abundance of species with environmental predictors, are essential tools for forecasting how species might respond to environmental changes, be they natural shifts or anthropogenic impacts.

Within the broad spectrum of available modeling techniques, Generalized Linear Models (GLM) and Generalized Additive Models (GAM) stand out as both foundational and transformative. While GLM extends the familiar linear regression to accommodate non-normally distributed response data, GAM further generalizes the relationship between predictors and responses by allowing for non-linearities via smooth functions. These characteristics make them particularly suited for capturing the complexities inherent in ecological datasets.

However, with their strengths come intricacies in interpretation, model selection, and diagnostics. Striking a balance between model complexity and ecological interpretability is an art as much as it is a science.

This book is conceived as a comprehensive guide to understanding and applying GLM and GAM in the context of SDMs. We will navigate through the theoretical underpinnings of these models, their implementation, and the challenges and solutions associated with their use. Real-world examples and case studies will illuminate the path, ensuring that the reader not only grasps the mathematical nuances but also appreciates their practical implications.

Embark with us on this exploration of the confluence of statistics and ecology, where GLM and GAM become powerful lenses through which we can better understand the distribution of life on our planet.

## GLM


```r
# Load required libraries
#install.packages("stats")
library(stats)

# Generate a hypothetical dataset
set.seed(123)
n <- 100
data <- data.frame(
  presence = rbinom(n, 1, 0.5),
  env1 = rnorm(n),
  env2 = rnorm(n)
)

# Fit a GLM
glm_model <- glm(presence ~ env1 + env2, data=data, family="binomial")

# Summary of the GLM
summary(glm_model)
```

```
## 
## Call:
## glm(formula = presence ~ env1 + env2, family = "binomial", data = data)
## 
## Coefficients:
##             Estimate Std. Error z value Pr(>|z|)  
## (Intercept)  -0.1426     0.2040  -0.699   0.4845  
## env1         -0.3646     0.2186  -1.668   0.0954 .
## env2         -0.0719     0.2189  -0.328   0.7426  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 138.27  on 99  degrees of freedom
## Residual deviance: 135.34  on 97  degrees of freedom
## AIC: 141.34
## 
## Number of Fisher Scoring iterations: 4
```

## GAM


```r
# Load required libraries
#install.packages("mgcv")
library(mgcv)
```

```
## Loading required package: nlme
```

```
## This is mgcv 1.8-42. For overview type 'help("mgcv-package")'.
```

```r
# Generate a hypothetical dataset (same as before)
set.seed(123)
n <- 100
data <- data.frame(
  presence = rbinom(n, 1, 0.5),
  env1 = rnorm(n),
  env2 = rnorm(n)
)

# Fit a GAM
gam_model <- gam(presence ~ s(env1) + s(env2), data=data, family="binomial")

# Summary of the GAM
summary(gam_model)
```

```
## 
## Family: binomial 
## Link function: logit 
## 
## Formula:
## presence ~ s(env1) + s(env2)
## 
## Parametric coefficients:
##             Estimate Std. Error z value Pr(>|z|)
## (Intercept)  -0.1241     0.2034   -0.61    0.542
## 
## Approximate significance of smooth terms:
##         edf Ref.df Chi.sq p-value  
## s(env1)   1      1  2.781  0.0954 .
## s(env2)   1      1  0.108  0.7426  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## R-sq.(adj) =  0.00925   Deviance explained = 2.12%
## UBRE = 0.41339  Scale est. = 1         n = 100
```

