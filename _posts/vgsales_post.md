---
date: '2023-03-15T20:32:40.138Z'
title: Video Game Sales App
tagline: 'R, Shiny App Development'
preview: >-
  Here, I created an Shiny App with R to visualize the differing sales
  distributions of the top 100 grossing games from 2010-2020.
image: 'https://source.unsplash.com/RMSLfydEKSI'
---
## Overview and Purpose

In this project, I created an interactive Shiny App using R to explore top grossing video game sales from 2010-2020. The data I used was amalgamated by Gregory Smith, and was hosted on Kaggle. Click [here](https://www.kaggle.com/datasets/gregorut/videogamesales) for a more detailed view of the dataset. 

## The App

You can interact with the app by clicking [here](https://lila-wells.shinyapps.io/Video_Game_Sales/?_ga=2.137736181.472847955.1677886303-1524006374.1677565427)

## Sneak Peek of the App 

Here are a few sneak peek of the app itself. 

### Part 1: Sales by Game Characteristics
![An old rock in the desert](https://images.unsplash.com/photo-1654475677192-2d869348bb4c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80)

![sales_by_characteristics](https://github.com/notlilawells/Video-Game-Sales-Shiny-App/blob/main/imgs/pt1.png)

This facet of the Video Game Sales Shiny app gives you insight into how the global sales of Kinect Adventures! relative to the average global sales of other games from the same genre, platform, publisher or year published. To operate this section of the app, choose a game in the first dropdown menu, then choose a method of comparison. Your choices are: 'Same Genre', 'Same Platform', 'Same Publisher', or 'Same Year Published'. The plot will then populate a bar for the global sales for the game you choose, as well as a bar representing the average sales for other games in that category

But wait! The table is also interactive! The table below the bar plot will also update to give you more information on the characteristics of the game you chose, here the example is Kinect Adventures! Now, go out and have some fun with this!

### Part 2: Sales by Region

![hi]('https://i.ibb.co/8zw66k8/sales-by-char-vgsales.png')

This facet of the Video Game Sales Shiny app gives you more detailed insights into the regional and global sales of Kinect Adventures! as well as where it was the most and least successful. To operate this section of the app, choose a game in the first dropdown menu, then select a sales region to highlight. Your choices are: 'North America', 'Europe', 'Japan', 'Other', or 'Global'. Note that choosing 'Global' will show you the game's total sales (as global sales encompass North American, European, Japanese, and other sales).

But what will clicking a sales region to highlight do? Let me tell you! The table below the bar plot updates automatically with your game choice to give you more insights into exactly how much the game sold in each of the sales regions. But what's especially interesting is that the text below the bar plot will update depending on the game of your choice, here the example is Kinect Adventures! The text will let you know now only how much the game sold in the region of your choice, but also what percentage that number is of the game's total global sales. Now, go out and have some fun with this!

## Skills
R, ggplot2, Shiny application development
