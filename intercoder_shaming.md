---
title: "Shaming project - reliability"
output: html_notebook
editor_options: 
  chunk_output_type: inline
---

For measuring intercoder reliability, check this [link](http://www.cookbook-r.com/Statistical_analysis/Inter-rater_reliability/)

### Initialize script
```{r echo=TRUE, message=FALSE, warning=FALSE}


library(tidyverse)
library(glue)
library(irr, quietly = T)


data_folder <- file.path("..", "data")
output_folder <- file.path("..", "output")
write_folder <- file.path("/", "Users", "radimhladik", "ownCloud", "erko", "shaming")

```

### Load data

Most data for calculating intercoder reliability are stored in a dedicated folder except for the Neural Monkey results, which have their own folder. This chunk simply loads relevants files. When new intercoder data arrive, they should be sourced here.

```{r}

source("src_intercoder/load_data.R")

```


## Reliability with Neural Monkey

This chunk calculates the scores for humans with the Neural Monkey classifier.
```{r echo=FALSE, warning=FALSE, message=FALSE}


source("src_intercoder/monkey.R", print.eval = TRUE, local=attach(.GlobalEnv))

```




## Reliability with lexicon - test no. 1

This chunk calculates the scores for humans with a rule-based lexicon method for sentiment detection. 150 items were coded by two human coders. The baseline lexicon sentiment is defined as:

* POS = NEG = 0 ~ "neutral"  
* POS = NEG ~ "neutral",
* POS > NEG ~ "positive",
* NEG > POS ~ "negative"


```{r echo=FALSE, message=FALSE, warning=FALSE}

source("src_intercoder/lex.R", print.eval = TRUE, local=attach(.GlobalEnv))


```

# Train NB on agreed data
```{r echo=FALSE, warning=FALSE, message=FALSE}

library(caret)

source("src_intercoder/classifier.R", print.eval = TRUE,  local=attach(.GlobalEnv))


```

## Prepare data to discuss coders' disagreements in round 1 of testing

```{r echo=FALSE, message=FALSE, warning=FALSE, include=FALSE}

source("src_intercoder/eval_test1.R", print.eval = TRUE,  local=attach(.GlobalEnv))


```




