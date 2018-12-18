# ConnectionsReassessmentRate---
---
title: "BAHCS-10 Prelim Results"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Library packages
```{r}
library(lavaan)
library(psych)
library(semTools)
library(dplyr)
library(ltm)
library(prettyR)
library(semTools)
library(GPArotation)
library(lavaan)
library(psych)
library(semTools)
library(dplyr)
library(ltm)
library(lordif)
library(Amelia)
library(plyr)
library(paran)
library(caret)
library(prettyR)
library(lme4)
#library(lmerTest)
library(MuMIn)
library(HLMdiag)
library(nlme)
library(MASS)
library(descr)
library(brms)
library(future)
```
Get rid of the 9 month reassessment rates
141 through 185 are between april and september for enrollments, so we never had a chance to get them
```{r}
setwd("C:/Users/Matthew.Hanauer/Desktop")
reassesData = read.csv("ConnectionsReassessment.csv", header = TRUE)

## Get rid of the 9 months 
describe.factor(reassesData$InterviewType) 
reassesData = subset(reassesData, InterviewType < 3)
dim(reassesData)
describe.factor(reassesData$InterviewType) 
reassesData$InterviewDate = as.Date(reassesData$InterviewDate, format = "%m/%d/%Y")

## Now subset for anyone with a 1 six months prior to October 1st so no one enrolled after April should be included in the reassessment rate
reassesData = reassesData[order(reassesData$InterviewType, reassesData$InterviewDate),]
head(reassesData)
reassesData = data.frame(ClientType = reassesData$InterviewType, InterviewDate = reassesData$InterviewDate)
head(reassesData)
describe(reassesData)
reassesData
reassesDataTest = reassesData[-c(139:186),]
describe.factor(reassesDataTest$ClientType)
110/138
```



