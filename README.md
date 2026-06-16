# Covid-19-Project

# 🦠 COVID-19 Global Trajectory Analytics & Forecasting

A comprehensive data science project analyzing global public health tracking data to uncover disease propagation patterns and forecast future cumulative cases — helping health analytics and resource planning teams anticipate pandemic curves.

## 📌 Problem Statement

Global public health organizations and resource planners face immense challenges in tracking, managing, and predicting the growth rate of pandemic curves. This project leverages historical daily tracking data to extract actionable insights on distribution dynamics and builds an automated time-series forecasting model to project future case trajectories.

## 📂 Dataset

| Feature | Description |
| --- | --- |
| **Date** | Observation date of the tracking log |
| **Country** | Country/Region of the recorded metrics |
| **State** | Province or state-level administrative partition |
| **Lat / Long** | Geographic latitude and longitude coordinates |
| **Confirmed** | Cumulative number of confirmed positive cases |
| **Deaths** | Cumulative number of recorded fatalities |
| **Recovered** | Cumulative number of clinically recovered patients |
| **Active** | Total active viral load cases undergoing treatment |
| **WHO Region** | Specified World Health Organization regional classification |

*Dataset size:* Continuous daily records tracking international administrative boundaries from early 2020 onwards, consolidating over 15.5 million historical cases by late July 2020.

## 🧹 Data Preprocessing

* Converted the `Date` column to proper datetime format and sorted records sequentially.
* Handled geographic fragmentation by performing temporal aggregations using `groupby(by='Date')` on cumulative metrics to construct a unified, global time-series timeline.
* Isolated specific early hot zones (such as China) into independent subset dataframes to analyze localized containment profiles.
* Formatted the target variables to meet the structural parameters of the forecasting model, mapping the time vector to `ds` and the cumulative target metric (`Confirmed`) to `y`.

## 📊 Exploratory Data Analysis — Key Insights

### 📉 Active Case Volatility

A highly asymmetrical distribution was observed across territories. A select group of major global hot spots drove the overwhelming majority of international active infection curves, highlighting severe localized stress on hospital infrastructures.

### 📅 Temporal Growth Trajectories

Global confirmed cases accelerated exponentially, expanding from a baseline of 555 cases on January 22, 2020, to over 15.5 million cumulative cases within a six-month window, emphasizing the critical need for advanced non-linear modeling.

### 🏥 Healthcare System Strain (Active vs. Recovered)

Contrasting real-time active infections against cumulative clinical recoveries successfully distinguished between nations that were systematically flattening their infection curves and those bearing critical infrastructure burdens.

### 🌏 Regional Containment Deviations

Early points of origin like China displayed unique logarithmic containment signatures that stabilized rapidly. This stood in stark contrast to the subsequent unmitigated exponential growth phases observed across western hemispheres.

## 🔮 Time Series Forecasting — Facebook Prophet

* Selected the globally aggregated cumulative case sequence to construct an optimized predictive modeling engine.
* Utilized an **Additive Regressive Model** (Facebook Prophet via PyStan) to accommodate non-linear piecewise growth trends and adapt to sudden curve trajectories (change points).
* Isolated **Weekly Seasonality** patterns to programmatically filter out administrative noise, such as weekend data entry backlogs or artificial mid-week reporting spikes.
* Trained the Prophet engine on the complete historical timeline to automatically compute trend parameters and growth coefficients.
* Extrapolated the model forward using target future date structures (`make_future_dataframe`) to compute point estimates (`yhat`).
* Generated 95% confidence intervals (`yhat_lower` and `yhat_upper`) to provide upper and lower uncertainty bands around the projected growth path.

## ✅ Conclusion

This project equips health resource coordinators and predictive analysts with:

* Actionable insights on macro-biological spread acceleration and peak reporting periods.
* Clear identification of regional trajectory deviations to help evaluate the real-world impact of containment policies.
* A forward-looking forecast featuring statistically backed uncertainty envelopes to proactively guide medical supply allocation and hospital capacity planning.

The Prophet model handles piecewise trend shifts and weekly administrative reporting lags seamlessly, making it highly effective for epidemiological trajectory forecasting.
