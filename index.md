---
layout: page
title Project 3
description: Description of Project 3.
nav_exclude: true
---

<script type="text/javascript" async="" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML"></script>

### Recipes and Rating Research Project

This is for Project 3 for DSC80 at UCSD
By Quinn Brandt

### Introduction

With diets and trends coming and leaving more frequently than ever, it is interesting to try to analyze those trends using the recipes and reviews users leave online. This proect attempts to start an analysis of some of these trends.

The two datasets used in this project originate from food.com, dating back to 2008. The first dataset contains recipes uploaded to food.com which includes columns such as recipe name, id, minutes to prepare, user id of the poster, recipe tags, nutrition information, number of steps, a description of the steps, and a user provided description. The second dataset contains user ratings of the recipes in the first dataset. This dataset includes columns usch as user id, recipe id, date of interaction, rating out of 5 stars, and a review.

The recipes dataset contains 83782 rows while the ratings dataset contains 731927 rows. Thus there are around 80,000 unique recipes and around 700,000 reviews. Thee first step to this project was to add an average rating column so we could analyze the popularity of certain types of recipes. 

There are a few different sections to this project. The first of which is to clean the data in order to use it in a smoother, easier to digest manner. This involves manipulating the format of multiple of the columns and even adding some columns.

Tied into cleaning is the exploratory data analyses. This involves univariate and bivariate analysis. This means looking at the distribution of important columns by themselves and in conjunction with other columns. We will also dive into aggregates to further examine the data.

The second step is to analyze the missingness of the data. This is split into two sections: NMAR and MCAR/MAR. The NMAR section I focused on the rating column while for the MCAR and MAR section we tested the dependency of the missingness of the review column. The two columns we explored for this were the minutes and number of steps columns.

Our overarching research question throughout this project relates to comparing the average ratings of different types of data. Specifically comparing the average rating of recipes classified as savory (greater than 75th percentile protein and less than 25th -percentile sugar) and sweet recipes (less than 25th percentile protein and greater than 75th percentile sugar).

As diet and obesity become a more prevelant topic in the US, it is important to analyze questions such as this to identify trends that may lead to poor diets. It also allows those creating recipes to cater to the likings of the general population better.