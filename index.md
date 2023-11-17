---
layout: page
title: Project 3
description: Description of Project 3.
nav_exclude: true
---

<script type="text/javascript" async="" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML"></script>

### Recipes and Rating Research Project

This is for Project 3 for DSC80 at UCSD

By: Quinn Brandt

---

### Introduction

With diets and trends coming and leaving more frequently than ever, it is interesting to try to analyze those trends using the recipes and reviews users leave online. This proect attempts to start an analysis of some of these trends.

The two datasets used in this project originate from food.com, dating back to 2008. The first dataset contains recipes uploaded to food.com which includes columns such as recipe name, id, minutes to prepare, user id of the poster, recipe tags, nutrition information, number of steps, a description of the steps, and a user provided description. The second dataset contains user ratings of the recipes in the first dataset. This dataset includes columns usch as user id, recipe id, date of interaction, rating out of 5 stars, and a review.

The recipes dataset contains 83782 rows while the ratings dataset contains 731927 rows. Thus there are around 80,000 unique recipes and around 700,000 reviews. Thee first step to this project was to add an average rating column so we could analyze the popularity of certain types of recipes. 

There are a few different sections to this project. The first of which is to clean the data in order to use it in a smoother, easier to digest manner. This involves manipulating the format of multiple of the columns and even adding some columns.

Tied into cleaning is the exploratory data analyses. This involves univariate and bivariate analysis. This means looking at the distribution of important columns by themselves and in conjunction with other columns. We will also dive into aggregates to further examine the data.

The second step is to analyze the missingness of the data. This is split into two sections: NMAR and MCAR/MAR. The NMAR section I focused on the rating column while for the MCAR and MAR section we tested the dependency of the missingness of the review column. The two columns we explored for this were the minutes and number of steps columns.

Our overarching research question throughout this project relates to comparing the average ratings of different types of data. Specifically comparing the average rating of recipes classified as savory (greater than 75th percentile protein and less than 25th -percentile sugar) and sweet recipes (less than 25th percentile protein and greater than 75th percentile sugar).

As diet and obesity become a more prevelant topic in the US, it is important to analyze questions such as this to identify trends that may lead to poor diets. It also allows those creating recipes to cater to the likings of the general population better.

---

### Data Cleaning and EDA

There were many steps in the data cleaning process. They included:
1. Merging the datasets
2. Replacing 0 values with Nan
3. Adding an average rating column
4. Converting strings to pandas datetime objects
5. Converting strings to lists when needed

The first step to this project was to merge the two dataframes and clean the data. the recipe id and id columns matched up and thus it was very simple to merge these dataframes.

Step two was replacing ratings of 0 with numpy NaN. The reasoning for this was that most ratings of 0 were due to reasons other than the recipe being bad. One example is people leaving comments on recipes they hadn't yet made who added a rating of 0.

Thirdly, I added an average rating column to the merged dataframe. I did this by creating a dictionary of recipe ids and their average rating, then creating a new column and mapping the dictionary onto the recipe id. 

The submitted and date columns of the dataframe were strings in the format of dates. I converted each of these to pandas date time objects, allowing them to be easier manipulated later.

The nutrition column was a string that looked like a list. I converted this to a list then made individual columns for each element of the list (calories, total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbs (PDV)). The columns tags and steps were also in the same format, however I did not convert these as they would not be necessary in my data analysis.

Lastly I replaced some should be null values in the columns. Primarily in the description and review columns, there were values that should have been null ('.', '...', '-', '1') so I found some of the most common and replaced them with null.

The head of the cleaned dataframe is shown below. I included only the inmportant columns for easier viewing.

| name                                 |     id |   minutes |   avg_rating |   calories |   protein (PDV) |   sugar (PDV) |
|:-------------------------------------|-------:|----------:|-------------:|-----------:|----------------:|--------------:|
| 1 brownies in the world    best ever | 333281 |        40 |            4 |      138.4 |               3 |            50 |
| 1 in canada chocolate chip cookies   | 453467 |        45 |            5 |      595.1 |              13 |           211 |
| 412 broccoli casserole               | 306168 |        40 |            5 |      194.8 |              22 |             6 |
| 412 broccoli casserole               | 306168 |        40 |            5 |      194.8 |              22 |             6 |
| 412 broccoli casserole               | 306168 |        40 |            5 |      194.8 |              22 |             6 |

# Univariate Analysis

In this section, I explored the distributions of individual columns. The first of which was the protein column. In doing so I found that the bulk of the recipes fell under one of two categories. The vast majority had between 0-20 percent of daily value protein. There was another peak in the data around 40-60 grams of protein.

<iframe src="assets/protein_hist.html" width=800 height=600 frameBorder=0></iframe>

Another histogram I looked at was the distribution of the average starts column. From this I found that the majority of recipes had between a 4 and 5 star rating. And there were high distributions at whole and half numbers. 

<iframe src="assets/star_hist.html" width=800 height=600 frameBorder=0></iframe>

# Bivariate Analysis

Bivariate analysis consists of comparing two of the columns together. The first way that I did this was to compare the protein and sugar columns. The main takeawy from this was that the two seemed to be negatively correlated with very few high protein meals also having high sugar and vice versa.

<iframe src="assets/pro_v_sug.html" width=800 height=600 frameBorder=0></iframe>

Another way that I used bivariate analysis was by comparing the minutes the recipe took and the length of the review left. From this you can see the there is a negative correlation between the two and the longer a recipe takes, the shorter the reviews are. 

<iframe src="assets/min_v_len.html" width=800 height=600 frameBorder=0></iframe>

# Interesting Aggregates

In this aggregate table, the index is stars rounded to the nearest whole number, and calories, protein, and sugar are all grouped by the aggregate function mean. It can be seen that the highest stars come from a moderate protein level and a low sugar level.

|   avg_rating |   calories |   protein (PDV) |   sugar (PDV) |
|-------------:|-----------:|----------------:|--------------:|
|            0 |    431.458 |         26.1583 |       71.0288 |
|            1 |    517.396 |         32.0761 |       97.6808 |
|            2 |    485.067 |         32.9594 |       92.5027 |
|            3 |    484.683 |         37.6013 |       82.6921 |
|            4 |    429.019 |         35.4949 |       62.6466 |
|            5 |    400.278 |         31.2887 |       60.0233 |

---

### Assessment of Missingness

# NMAR

IDK yet

# Missingness Analysis

The review columns is one of three that had many instances of missing values. I noticed that it appeared to be dependent on the number of steps column. I first created a new dataframe with only the rows that had missing review values and took the mean of the number of steps. Then I took the original dataframe and took the mean of the number of steps. The absolute difference between these two came out to about 4.83. I then ran a permutation test where I shuffled the review column 500 times and took the absolute difference of means each time. I found that 0% of the 500 trials had an absolute difference equal to or greater than the test statistic. 

<iframe src="assets/steps_perm_hist.html" width=800 height=600 frameBorder=0></iframe>

I the ran another permutation test using the minutes column. I originally expected this to have a similar result as the number of steps permutation test. I ran the same test, shuffling the review column 500 times. I got an absolute difference in minutes of about 23.23 as the test statistic. After running the permutation test, I found that about 81.8% of the results were equal to or greater than the test statistic.

<iframe src="assets/mins_perm_hist.html" width=800 height=600 frameBorder=0></iframe>

### Hypothesis Testing

The question I chose to explore was whether sweet or savory recipes had a higher average rating. I defined sweet recipes as those with 75th percentile or higher sugar and 25th percentile or lower protein. Savory recipes are defined as 75th percentile or higher protein and 25th percentile or lower sugar. I used a permutation test to evaluate this question.

# Set Up

Null Hypothesis: Both sweet and savory recipes are rated the same by reviewers.

Alternative Hypothesis: Reviewers rate sweet and savory recipes differently.

For this I first found a test statistic by creating two filtered datasets. One with only savory meals, and the other with only sweet meals. I calculated the mean of the average stars column in each and then took the absolute difference giving me a test statistic of of about 0.054. I chose a p-value of 0.05.

I then ran a permutation test in which I shuffled the average rating column. Then created the same two datasets as above and took the means. I took the absolute difference and added it to a list. I repeated those steps 500 times and found that the number of absolute differences that were greater than or equal to my test statistic was 0. Thus I was able to reject the null hypothesis. 

<iframe src="assets/hyp_his_hist.html" width=800 height=600 frameBorder=0></iframe>
