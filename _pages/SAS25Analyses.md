---
title: "SAS 2025 Analyses"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
{library(tidyverse)
  library(readxl)
  library(openxlsx)
  library(plyr)
  library(dplyr)
  library(tidyr)
  library(data.table)
  library(psych)
  library(lme4)
  library(lmerTest)
  library(ggplot2)
  library(sjPlot)
  library(sjmisc)
  library(performance)
  library(effects)
  library(interactions)
}
```

```{r, echo=FALSE}
long_data <- read.csv("/Users/ipeckinpaugh2/Downloads/checked.Long_data_mddriskcvbproject02.10.25.csv")
long_data <- long_data |> 
  mutate(risk_dummy = case_when(
    risk == "low-risk" ~ 0,         # low-risk becomes 0
    risk == "high-risk" ~ 1,        # high-risk becomes 1
  )) 
long_data <- long_data |> 
  mutate(sex_dummy = case_when(
    sex == "F" ~ 0,         # low-risk becomes 0
    sex == "M" ~ 1,        # high-risk becomes 1
  )) 
```
# Model 1
## _(H1) High-risk offspring will have greater symptoms of depression_
```{r, echo=FALSE}
Model <-lmer(RCADS.MD~ risk_dummy+Age_kid +sex_dummy  + (1  | kID) , data=long_data)
summary(Model)
```

# Model 2
## _(H2) High-risk offspring will have worse reappraisal habits and (H4; exploratory) age will moderate this relationship_
```{r, echo=FALSE}
Model <-lmer(ERQCA.R~ as.factor(risk_dummy)*Age_kid  + sex_dummy+ (1  | kID) , data=long_data) 
  summary(Model)
```

## High-risk offspring reported worse reappraisal habits than low-risk individuals up until 15 years of age.
```{r, echo=FALSE, warning=FALSE}
 plot_model(Model, type="pred", terms= c("Age_kid", "risk_dummy"), colors = c("dodgerblue","coral2")
            ) + theme_minimal() +
    theme(
      panel.background = element_rect(fill="white", color=NA),
      plot.background = element_rect(fill = "white", color = NA),  # Set outer plot area background to black
      panel.grid = element_blank(),  # Remove gridlines
      axis.text = element_text(color = "black"),  # Change axis text color for visibility
      axis.title = element_text(color = "black"),
      axis.title.y = element_text(size=20),
      axis.title.x = element_text(size=20),
      axis.line.x = element_line(color="black"),
      axis.line.y = element_line(color="black"),
      legend.position  = "none",
      axis.text.x  = element_text(size=15),
      axis.text.y  = element_text(size=15)
    ) + labs(x = "Offspring Age",
           y = "Reappraisal Habit", legend = "Risk" ) 
  
```
<br>

## The relationship between risk and reappraisal was significant up until age 12.
```{r, echo=FALSE, warning=FALSE}
long_data$risk_dummy <- as.numeric(as.character(long_data$risk_dummy))
Model <- lmer(ERQCA.R ~ risk_dummy + Age_kid + risk_dummy:Age_kid + sex_dummy + (1 | kID), data = long_data)

my_sim_slopes <- sim_slopes(
  Model,
  pred = risk_dummy,
  modx = Age_kid,
  jnplot = TRUE,
  mod.range = c(6.00, 23.00),
 sig.color = "turquoise2",insig.color = "grey",
  confint = TRUE
)

plot <- my_sim_slopes[["jnplot"]]
plot[["layers"]][c(7)] <- NULL
plot +
  labs(title = NULL,
       x = "Offspring Age",
       y = "Conditional Effect of Risk on Reappraisal Habit") +
  theme(legend.position = "bottom", text = element_text(size = 10),
        axis.title.y = element_text(size=15),
        axis.title.x = element_text(size=20), 
        legend.text=element_text(size=15),
        axis.text.x = element_text(size=18),
        axis.text.y = element_text(size=15))
```


# Model 3
## _(H3) Worse reappraisal habits will predict greater depression symptoms and (H5; exploratory) age will moderate this relationship_
```{r, echo=FALSE}
Model <- lmer(RCADS.MD~ Age_kid*ERQCA.R  + sex_dummy+ (1  | kID) , data=long_data)
summary(Model)
```

## The relationship between reappraisal habits and depression symptoms was significant after age 12
```{r, echo=FALSE, warning=FALSE}
long_data$risk_dummy <- as.numeric(as.character(long_data$risk_dummy))
Model <- lmer(RCADS.MD~ Age_kid+ERQCA.R  + sex_dummy+ Age_kid:ERQCA.R + (1  | kID) , data=long_data)

my_sim_slopes <- sim_slopes(
  Model,
  pred = ERQCA.R,
  modx = Age_kid,
  jnplot = TRUE,
  mod.range = c(6.00, 23.00),
  sig.color = "turquoise2",insig.color = "grey",
  confint = TRUE
)

plot <- my_sim_slopes[["jnplot"]]
plot[["layers"]][c(7)] <- NULL
plot +
  labs(title = NULL,
       x = "Offspring Age",
       y = "Conditional Effect of Reappraisal on Depression Symptoms") +
  theme(legend.position = "bottom", text = element_text(size = 10),
        axis.title.y = element_text(size=10),
        axis.title.x = element_text(size=20), 
        legend.text=element_text(size=15),
        axis.text.x = element_text(size=18), 
        axis.text.y = element_text(size=15))

```


# Model 4 
##(H6; exploratory) Directionality of the effects are such that risk will predict future depression symptoms and future ER difficulties
```{r, echo=FALSE, warning=FALSE}
lag_data <- read.csv("/Users/ipeckinpaugh2/Downloads/lag_data_sas25_3.4.25.csv")
```

```{r, echo=FALSE, warning=FALSE}
timelag<-lm(RCADS.MD.T2~ RCADS.MD.T1 + as.factor(risk.T1) + Age.T2 , data=lag_data)
summary(timelag)
```

# Model 5
## (H6; exploratory) Directionality of the effects are such that risk will predict future depression symptoms and future ER difficulties
```{r, echo=FALSE, warning=FALSE}
timelag<-lm(ERQCA.R.T2~ ERQCA.R.T1 + as.factor(risk.T1) + Age.T2, data=lag_data)
summary(timelag)
```

