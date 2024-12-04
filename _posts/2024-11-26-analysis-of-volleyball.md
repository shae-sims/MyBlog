---
layout: post
title:  "What Determines a Players Rank?"
author: Shaelyn Eldrege
description: Looking into what determines the rank of a volleyball player in the Big 10 Conference using data from the 2023 colleigate season and creating a streamlit app.
image: /assets/images/volleyballbeach.jpg
display_image: True
---

## Introduction

Volleyball has always been a love of mine. It is one of the reasons I decided to persue a degree in statistics. I wanted to be able to analyze and make predictions based of off the data that is kept during volleyball games. One thing I have always found interesting is player rankings. Why do certain players get ranked higher? What skill is the most valued when looking at rankings?

These are a few questions and more that can be answered by looking at the Big 10 Conference volleyball player rankings from 2023. You can view these rankings online <a href="https://bigten.org/wvb/stats/" target="_blank">here</a>. We will be exploring the answers to these questions and how to use it to make an interactive streamlit app to explore the data even further.


## Exploring the Data

The first thing I did to explore this data is look into the correlation between all of the numeric variables in the data set. These variables include kills, assists, aces, blocks and digs. The correlation can tell us which variables are related to another.

<img src="{{site.url}}/{{site.baseurl}}/assets/images/correlationmatrix.png" alt="" style="display: block; margin: auto;"/>

As shown above in the correlation matrix the skill most correlated with rank is total number of kills and kills per set. This indicates to us that compared to any other skill the one that has the highest affect on ranking is the offensive attack. *A kill is when you get a point off of hitting the ball.* This shows that ranks are affected by points scored. *The other skills do not generally result in a point, besides aces*

Another interesting trend we can see in the data is between aces and digs. We can see the relationship of these two skills by look at the correlation coefficient, which is 0.7, and by looking at the scatterplot between the two points.

<img src="{{site.url}}/{{site.baseurl}}/assets/images/onlydigsandaces.png" alt="" style="display: block; margin: auto;"/>

There is a clear upward trend. This is interesting because every player on the court takes a turn serving the ball. However, the best servers also seem to be those who do well in the back row.

## The Streamlit App

To be able to explore the data even more we can use a streamlit app. To see the data and the code to make this app you can go to this <a href="https://github.com/shae-sims/volleyballapplication/tree/main" target="_blank">github repository</a>

