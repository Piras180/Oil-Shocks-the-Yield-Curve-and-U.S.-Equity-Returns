# Oil Shocks, the Yield Curve, and U.S. Equity Returns

**Empirical Methods in Finance | HEC Lausanne | 2026**  
**Research area:** Financial econometrics · Macroeconomic risk · Equity return forecasting

## Overview

Can oil-price shocks help predict U.S. equity returns once changes in the Treasury yield curve are taken into account?

This academic research project examines the relationship between **WTI crude oil returns**, **S&P 500 returns**, and changes in the **U.S. 10-year minus 2-year Treasury yield spread**. Using weekly observations from **January 1990 to March 2026**, it investigates both the economic transmission mechanism and whether the proposed predictors improve *out-of-sample* forecasts.

**Main conclusion:** Although some relationships are statistically significant in-sample, the models that use oil and yield-curve information do **not** outperform a simple zero-return (random-walk) benchmark in the rolling forecast exercise. The estimated oil–equity relationship also changes across market regimes.

## Research approach

The work covers four stages:

1. **Data preparation and diagnostics:** Resample daily observations to Friday frequency; compute weekly log returns and changes in the 10Y–2Y spread; assess normality, serial correlation, volatility clustering, and cross-asset correlations.
2. **Econometric modelling:** Estimate an OLS baseline and dynamic return models. The notebook implements **ARMAX(1,1)** using a custom Gaussian likelihood and numerical maximum-likelihood estimation, including outer-product-of-gradients (OPG) standard errors. The written report also evaluates **ARX(1)** and **VAR(1)** specifications.
3. **Out-of-sample evaluation:** Re-estimate models using a **156-week rolling training window**, generate one-week-ahead forecasts, and compare forecast errors with AR(1) and zero-return benchmarks.
4. **Regime analysis:** Track rolling root mean squared error (RMSE) and time-varying oil coefficients through periods including the 2008 financial crisis, COVID-19, and the 2022 inflation and rate-hiking cycle.

## Selected results

### Forecast accuracy — Python notebook

Based on **1,731 rolling weekly forecasts** (approximately 1993–2026):

| Model | Out-of-sample RMSE | RMSE versus zero-return benchmark |
| --- | ---: | ---: |
| Zero-return / random-walk benchmark | **0.023680** | Baseline |
| AR(1) | 0.023918 | 1.01% higher |
| ARMAX(1,1) | 0.024501 | 3.47% higher |

The **written report** evaluates an alternative model set and reports RMSEs of **0.024370 for ARX(1)** and **0.024383 for VAR(1)**, versus **0.023680** for the same benchmark. In both comparisons, the simpler forecast is more accurate on average.

### Other findings

- **In-sample relationship:** The OLS baseline finds a negative coefficient on lagged yield-spread changes (**−0.0202; p = 0.0027**), while lagged oil returns are not significant in that specification (**p = 0.4099**). The model's explanatory power is low (**R² = 0.56%**).
- **Sensitivity to model specification:** The dynamic models produce materially different coefficient estimates, underscoring the importance of modelling return dependence rather than relying on a single static regression.
- **Regime dependence:** Rolling oil coefficients vary in magnitude and sign over time, making a single stable oil-to-equity forecasting relationship difficult to establish.
- **Practical implication:** An economically plausible signal does not necessarily improve out-of-sample prediction. Forecasts should be assessed against transparent, simple benchmarks.

## Repository contents

| File | Description |
| --- | --- |
| [`FINAL (1).ipynb`](FINAL%20%281%29.ipynb) | Python notebook with data preparation, manually implemented OLS, ARMAX likelihood estimation, rolling forecasts, diagnostics, and visualisations. |
| [`Report (3).pdf`](Report%20%283%29.pdf) | Full academic report, including motivation, literature review, ARX/VAR analysis, results, and limitations. |
| `README.md` | Project overview and selected findings. |

**Implementation note:** The notebook and the report share the same research question and underlying data, but they use **different dynamic model specifications**. In particular, the uploaded notebook does not reproduce the report's VAR(1) and impulse-response analysis. Their numerical results should therefore be read as separate implementations, not as identical computational outputs.

## Tools and skills demonstrated

**Python:** `numpy`, `pandas`, `scipy`, `statsmodels`, `matplotlib`, Jupyter Notebook  
**Quantitative methods:** OLS estimation, ARMAX maximum likelihood, numerical optimisation, OPG standard errors, residual diagnostics, rolling-window estimation, RMSE benchmarking, and time-varying coefficient analysis  
**Finance applications:** Equity-return forecasting, macro-financial linkages, yield-curve analysis, and model-risk assessment

## Reproducing the notebook

The notebook expects an Excel input file named **`data_hec_projet_1.xlsx`** in the same directory, containing a worksheet named **`Daily`** with the required market series. This data file is **not included** in the uploaded repository materials; access to it is necessary to rerun the analysis.

Install the main dependencies:

```bash
python -m pip install jupyterlab numpy pandas scipy statsmodels matplotlib openpyxl
```

Then open the notebook:

```bash
jupyter lab "FINAL (1).ipynb"
```

Run the cells in order after placing a properly formatted dataset in the project directory. The rolling optimisation performs a large number of model fits, so full execution can be computationally intensive. Check any data redistribution restrictions before committing the original dataset to a public repository.

## Limitations

The analysis uses reduced-form statistical relationships rather than causally identified oil supply and demand shocks. Weekly aggregation may miss faster market reactions. Model coefficients are sensitive to changing market conditions, and the overall out-of-sample results do not demonstrate an exploitable forecasting signal.

## Authors

**Matteo Piras, Marco D’Amico, and Roberto Berardi**  
Academic group project — *Empirical Methods in Finance*, HEC Lausanne (2026).
