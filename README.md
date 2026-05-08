# Bitcoin Price Movements: Volume, Volatility & Halving Cycles (2013–2025)

## Research Question

How do trading volume and market volatility explain Bitcoin's daily price 
movements across halving cycles and seasonal patterns between 2013 and 2025?

## Overview

This project investigates whether trading volume, 30-day rolling volatility, 
Bitcoin halving cycles, and seasonal patterns help explain the **magnitude** 
of daily Bitcoin returns. The dependent variable is the absolute value of 
daily returns |daily_return|, capturing price instability independently of 
direction.

## Data Source

Bitcoin historical daily data (2013–2025) from Kaggle:  
https://www.kaggle.com/datasets/adilshamim8/bitcoin-historical-data

## Methods

- Exploratory Data Analysis (distributions, boxplots, ridgeline plots, correlation matrix)
- 30-day rolling volatility window on log-returns
- Kruskal–Wallis and Dunn post-hoc tests for group comparisons
- Linear regression: `abs_return ~ log(volume) + volatility_30d + halving_cycle + season`
- Model diagnostics: Residuals vs Fitted, QQ plot, Breusch–Pagan test

## Key Findings

- Trading volume and volatility are significant positive predictors of return magnitude
- Halving cycles capture structural regime differences in Bitcoin market behavior
- Seasonal effects are weak once volume and volatility are controlled for
- Heteroskedasticity is present and consistent with the nature of crypto markets

## Repository Structure
btc-volume-volatility-returns/
├── Bitcoin_history_data.csv      # Raw dataset
├── btc_analysis.Rmd              # Main R project (analysis + code)
├── ai_pipeline.md                # AI tool usage log
└── README.md

## Tools & Libraries

R · tidyverse · ggplot2 · ggridges · corrplot · lubridate · FSA · lmtest · zoo

## Academic Context

Capstone project — Preparatory Program, University of Basel (FS26)
