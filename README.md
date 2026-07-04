# Bitcoin Price Movements: Volume, Volatility & Halving Cycles (2013–2025)

A quantitative analysis of Bitcoin daily price instability using volatility modeling, structural regime comparison, and regression diagnostics.

## Motivation

This project was built to explore how market activity and risk conditions explain short-term price instability in a highly volatile, structurally evolving asset like Bitcoin. The objective is to test whether trading volume, rolling volatility, halving-driven supply regimes, and calendar seasonality are associated with the magnitude of daily BTC price movements, and to evaluate how well a standard linear model captures that relationship once tested against its own assumptions.

## What the Project Does

The analysis is divided into four main stages:

### 1. Data Pipeline
Daily BTC price and volume data (2013–2025) is sourced from Kaggle and cleaned in R. Log-returns are computed, and a 30-day rolling standard deviation of log-returns is used to construct a volatility measure. Two structural/categorical features are engineered: a four-regime halving-cycle indicator (based on the 2016, 2020, and 2024 halving dates) and a calendar-season indicator.

### 2. Exploratory Data Analysis
Distributions of absolute returns, log-volume, and volatility are examined for skewness. Volatility is compared across halving cycles, seasons, and months via boxplots and a monthly trend line. A ridgeline plot visualizes how the volatility distribution has shifted year over year, and a correlation matrix quantifies the linear relationships between absolute returns, volatility, and volume.

### 3. Group Comparison Tests
Since volatility is not normally distributed, non-parametric tests are used: a Kruskal–Wallis test evaluates whether volatility differs across halving cycles (it does, with Dunn's post-hoc test identifying which cycles differ most), and a second Kruskal–Wallis test checks trading volume across seasons (no significant difference found).

### 4. Regression & Diagnostics
A linear model regresses absolute daily returns on log-volume, 30-day volatility, halving cycle, and season:
```
abs_return ~ log(volume) + volatility_30d + halving_cycle + season
```
Model assumptions are then stress-tested: a Residuals-vs-Fitted plot and a QQ plot check for heteroskedasticity and non-normality, and a Breusch–Pagan test formally confirms the presence of heteroskedasticity in the residuals.

## Key Findings

* Trading volume and 30-day volatility are both significant, positive predictors of daily return magnitude — periods of intense activity and elevated risk produce larger price swings.
* Halving cycles capture real structural differences in Bitcoin's behavior, with volatility increasing across later regimes even after controlling for volume and volatility.
* Seasonal effects are weak and largely disappear once volume and volatility are controlled for, consistent with Bitcoin's continuous, global trading structure.
* The model shows clear heteroskedasticity (Breusch–Pagan test, p < 2.2e-16) and fat-tailed residuals (QQ plot) — expected properties of financial return data that motivate a future extension using robust standard errors or a GARCH-type volatility model.

## Tech Stack

* R
* tidyverse
* ggplot2 · ggridges
* corrplot
* lubridate
* FSA (Dunn's test)
* lmtest (Breusch–Pagan test)
* zoo (rolling volatility)

## Data Source

Bitcoin historical daily data (2013–2025) from Kaggle:
https://www.kaggle.com/datasets/adilshamim8/bitcoin-historical-data

## How to Run

1. Clone the repository and place `Bitcoin_history_data.csv` in the project root.
2. Open `Bitcoin_Volatility_Halving_Cycles_Analysis.Rmd` in RStudio.
3. Install any missing packages (see Tech Stack above).
4. Knit the document to HTML to reproduce the full analysis, from data wrangling through regression diagnostics.

## Academic Context

Capstone project — Preparatory Program, University of Basel (FS26).
