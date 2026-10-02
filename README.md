# Investment Deflator Inflation — ARDL and Cointegrated VAR

A University of Bologna econometrics course report examining investment-deflator inflation alongside domestic value-added inflation adjusted for indirect taxes and import-price inflation.

## Scope and methods

The report documents preliminary time-series plots and ADF tests, Hodrick–Prescott filtered gaps, VAR and impulse-response analysis, an ARDL specification, Engle–Granger residual testing, and Johansen cointegration analysis. It also refers to Pesaran–Shin–Smith (PSS) bounds testing, but does not provide a bounds-test statistic and critical-value table. The report describes a cointegrated VAR; this repository does not include material sufficient to verify a separate VECM implementation.

## Reported results and limits

The report presents positive ARDL/Engle–Granger associations for domestic-cost and import-price measures, but its Johansen discussion gives a different sign for imports and reports no long-run role for the domestic-cost measure. Its ADF table and accompanying interpretation also conflict, and some described tests lack the underlying output needed to check the claims. These are claims reported in the document, not independently verified findings. The repository does not establish causal effects or support forecasts.

## Report

- [`Group10_Investment_Deflator_Econometrics_Report.pdf`](Group10_Investment_Deflator_Econometrics_Report.pdf) — the project report. Student identifiers visible on the cover have been removed, and PDF author metadata now matches the credited authors; the report authorship is retained.

## Scope and reproducibility

This repository contains the PDF report and this README only. The original source data, analysis code, and a machine-readable replication workflow are absent, so the reported analysis cannot be independently reproduced from this repository alone. Treat it as an academic case study in applied time-series econometrics, not a reusable forecasting tool.

- **Academic context:** Econometrics course, University of Bologna
- **Authors:** Atabak Nikouseresht, Mahgol Lamei, and Kimia Shokri
