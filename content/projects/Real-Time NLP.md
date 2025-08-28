---
title: "Real-Time NLP to track public opinion"
date: 2025-07-11
description: "Using social media post data to estimate public opinion of specific entities"
tags: ["TextBlob", "NLP", "pandas", "Data Science", "ML"]
---

# Overview - Social Media are generally terrible investors: #
Economic reasons for this are varied and not generally the point of this project - most social media favourites are volatile stocks with inflated or deflated values that makes investing in them risky.
The aim of this project was to create a leaderboard to track a given community's perceptions of stocks - potentially enabling an inverse fund which buys when opinion is negative, sells when positive.

# Development #
## Scraping Social Media posts ##
Most social media will have specific APIs to scrape posts pertaining to specific topics or communities - for the sake of efficiency, I chose reddit's r/wallstreetbets as it has a proven track record of poor investment selection - and also routinely includes specific stock tickers in titles i.e. :
"so bullish on AAPL this week guys, earnings report looking good"
reddit's API is free up to a daily limit so no issues with scraping incrementally and merging over time.

## Processing posts ##
From here, I was able to write a function to scrape all posts from r/wallstreetbets and a separate function to convert that post into a weighted dict of stock tickers : community sentiments
This works by taking the title, scraping any tickers out that are in the NYSE ticker dataset and extracting sentiments about those tickers using TextBlob - these values are then weighted by post karma to get an idea of how much the community agrees with this sentiment.

## Iteration & improvements ##
Opinions tend to change quickly online, especially in financial social media - strong positive opinions could be overcome very quickly; I decided to update the model to have sentiments decay over time:
I updated the model to apply a coefficient of 0.9 to existing sentiments every day - simulating this decay of opinion.

