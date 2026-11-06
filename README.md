# German Electricity Market Analysis: Renewable Generation and Day-Ahead Electricity Prices

## Project Overview

This project investigates the relationship between renewable electricity generation and day-ahead electricity prices in Germany. Using Python, I collected and analysed electricity generation and market price data to explore how variations in wind and solar power generation relate to wholesale electricity prices.

The analysis focuses on identifying patterns in renewable energy production, examining electricity price volatility, and evaluating the relationship between combined wind and solar generation and electricity prices.

The project demonstrates the application of Python-based data analysis to energy-market research and explores the relevance of renewable energy availability to electricity pricing and trading.

## Objectives

The main objectives of this project were to:

- Retrieve and process German electricity generation and day-ahead price data.
- Examine the temporal patterns and variability of wind and solar electricity generation.
- Analyse fluctuations in German day-ahead electricity prices, including negative and exceptionally high prices.
- Investigate the relationship between renewable electricity generation and wholesale electricity prices.
- Evaluate how average electricity prices differ across varying levels of renewable generation.
- Explore the relevance of renewable generation patterns to electricity-market dynamics.

## Data Sources

The analysis uses data retrieved from the **Fraunhofer Energy-Charts API (v2)**.

Two datasets were collected:

1. **Electricity Generation Data:** German electricity generation observations, including solar, onshore wind and offshore wind generation.
2. **Day-Ahead Electricity Price Data:** German day-ahead electricity market price observations.

The datasets cover the period from **1 November 2025 to 5 November 2026**, based on the timestamps in the processed dataset.

After preprocessing and integration, the final dataset contained **8,880 hourly observations** and four analytical variables.

## Tools and Technologies

- **Python:** Primary programming language.
- **Pandas:** Data extraction, cleaning, transformation, time-series resampling and dataset integration.
- **NumPy:** Numerical operations.
- **Matplotlib:** Time-series visualisation and chart customisation.
- **Seaborn:** Statistical data visualisation.
- **Fraunhofer Energy-Charts API:** Electricity generation and market price data retrieval.

## Methodology

The project followed a structured data-analysis workflow.

### 1. Data Collection and Extraction

Electricity generation and day-ahead price data were retrieved from the Energy-Charts API.

A reusable Python function was developed to extract timestamps and corresponding observations from the API responses and convert them into Pandas DataFrames.

Timestamps were converted from UTC to the `Europe/Berlin` time zone to align the analysis with German local time.

### 2. Data Cleaning and Preparation

The generation dataset was processed to identify solar, onshore wind and offshore wind variables.

The following analytical variables were created:

- `solar_mw`: Solar electricity generation.
- `wind_mw`: Combined onshore and offshore wind generation.
- `wind_solar_mw`: Combined wind and solar generation.
- `price_eur_mwh`: Electricity price in EUR/MWh.

Combined wind generation was calculated by summing the available wind generation columns, while combined renewable generation was calculated as the sum of solar and wind generation.

### 3. Time-Series Aggregation and Integration

Both datasets were resampled to hourly intervals using arithmetic averages.

The hourly generation and price datasets were then joined using their timestamps. An inner join was applied to retain only matching observations, and incomplete records were removed.

The resulting analytical dataset contained:

| Variable | Description | Unit |
|---|---|---|
| `solar_mw` | Solar electricity generation | MW |
| `wind_mw` | Combined wind generation | MW |
| `wind_solar_mw` | Combined wind and solar generation | MW |
| `price_eur_mwh` | Average electricity price | EUR/MWh |

**Final dataset size: 8,880 observations × 4 variables.**

### 4. Exploratory Data Analysis

Exploratory analysis was conducted to understand the distribution and variability of electricity generation and prices.

Descriptive statistics, including the mean, median, standard deviation, minimum, maximum and quartiles, were calculated.

Time-series visualisations were also created to examine:

- Hourly fluctuations in German day-ahead electricity prices.
- Daily average wind electricity generation.
- Daily average solar electricity generation.
- Seasonal patterns and variations in renewable electricity production.

### 5. Correlation Analysis

Pearson and Spearman correlation coefficients were calculated to investigate the direction and strength of the relationships between wind generation, solar generation, combined renewable generation and electricity prices.

- **Pearson correlation:** Evaluates the strength and direction of linear relationships.
- **Spearman correlation:** Evaluates the strength and direction of monotonic relationships using ranked observations.

Using both measures provides complementary perspectives on the observed relationships.

### 6. Renewable Generation Segmentation

Combined wind and solar generation observations were divided into four equally sized groups using quartile-based segmentation:

- Low
- Moderate-low
- Moderate-high
- High

The mean and median electricity prices were then calculated for each group to examine how market prices varied across different levels of renewable generation.

## Key Findings and Results

### 1. Electricity Price Characteristics

The descriptive analysis revealed considerable variation in German day-ahead electricity prices.

| Statistic | Result |
|---|---:|
| Mean price | €113.20/MWh |
| Median price | €110.00/MWh |
| Standard deviation | €67.82/MWh |
| Minimum price | -€499.00/MWh |
| Maximum price | €697.31/MWh |

The observed negative and exceptionally high prices demonstrate the volatility present in the analysed electricity-market data.

### 2. Renewable Electricity Generation

The average generation levels during the study period were:

| Generation source | Mean generation |
|---|---:|
| Solar | 9,619.73 MW |
| Wind | 16,065.50 MW |
| Combined wind and solar | 25,685.23 MW |

The visual analysis revealed substantial variability in wind generation and a seasonal pattern in solar generation, with higher solar output generally observed during the spring and summer months.

### 3. Correlation Between Renewable Generation and Electricity Prices

The correlation analysis revealed negative associations between renewable electricity generation and day-ahead electricity prices.

| Variable | Pearson correlation | Spearman correlation |
|---|---:|---:|
| Wind generation | -0.290 | -0.320 |
| Solar generation | -0.480 | -0.323 |
| Combined wind and solar generation | **-0.662** | **-0.684** |

The strongest negative association was observed between combined wind and solar generation and electricity prices.

The results suggest that higher combined renewable generation tends to coincide with lower electricity prices in the analysed dataset.

### 4. Electricity Prices Across Renewable Generation Groups

Quartile-based segmentation revealed a clear downward pattern in average electricity prices as renewable generation increased.

| Renewable generation group | Mean price (EUR/MWh) | Median price (EUR/MWh) | Observations |
|---|---:|---:|---:|
| Low | 162.67 | 148.34 | 2,220 |
| Moderate-low | 134.52 | 126.00 | 2,220 |
| Moderate-high | 108.43 | 101.54 | 2,220 |
| High | 47.20 | 47.23 | 2,220 |

Average electricity prices were approximately **71% lower during high renewable-generation hours compared with low renewable-generation hours**.

This finding is consistent with the merit-order effect, whereby increased availability of low-marginal-cost renewable electricity can displace more expensive generation and put downward pressure on wholesale electricity prices.

## Discussion and Energy-Market Relevance

The findings highlight the importance of renewable electricity generation as a variable in understanding wholesale electricity-market behaviour.

Wind and solar generation are weather-dependent and can fluctuate considerably over time. Changes in renewable electricity availability can influence the supply balance and contribute to movements in market prices.

The observed negative relationship between combined renewable generation and electricity prices illustrates the potential relevance of renewable generation data in:

- Electricity price analysis and market monitoring.
- Renewable energy forecasting.
- Understanding supply-side influences on wholesale electricity prices.
- Assessing periods of potential price pressure.
- Supporting data-driven energy-market research and trading analysis.

These findings provide an exploratory view of the relationship between renewable generation and electricity prices rather than a predictive trading strategy.

## Limitations

Several limitations should be considered when interpreting the results:

1. **Correlation does not imply causation:** The analysis identifies statistical associations but does not establish that renewable generation directly causes electricity price movements.
2. **Electricity demand:** Demand was not included as an explanatory variable, although it is an important determinant of electricity prices.
3. **Other market fundamentals:** Fuel prices, carbon prices, power plant availability, cross-border electricity flows and other market conditions were not explicitly modelled.
4. **Historical analysis:** The project investigates historical patterns and does not currently forecast future electricity prices.
5. **Hourly aggregation:** Averaging observations into hourly intervals simplifies the comparison but may obscure shorter-term price movements and differences in the original market settlement intervals.

## Conclusion

This project demonstrates how Python-based data analysis can be applied to investigate the relationship between renewable electricity generation and wholesale electricity prices.

The analysis of 8,880 hourly observations revealed a moderately strong negative association between combined wind and solar generation and German day-ahead electricity prices (Pearson correlation = -0.662; Spearman correlation = -0.684).

The quartile analysis further showed that average electricity prices were approximately 71% lower during high renewable-generation hours than during low renewable-generation hours.

Overall, the findings highlight the relevance of renewable electricity availability to electricity-market dynamics and provide a foundation for further analysis of energy-market fundamentals.

## Potential Future Improvements

Further development could extend the analysis by:

- Incorporating electricity demand and load data.
- Examining the influence of natural gas and carbon prices.
- Investigating the relationship between renewable generation and negative electricity prices.
- Comparing weekday and weekend market behaviour.
- Developing regression models to evaluate the influence of multiple market variables.
- Exploring machine-learning approaches for electricity price forecasting.

## Author

**Adebola David Adedayo**

MSc Geospatial Technologies | Data Analytics | Python | Energy-Market Analysis

[LinkedIn](https://www.linkedin.com/in/adebola-adedayo/) | [GitHub](https://github.com/adebolaadedayo)
