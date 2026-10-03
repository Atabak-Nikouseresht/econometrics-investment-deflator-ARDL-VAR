# Errata and Interpretation Notes

## Purpose

This is a documentation review of [Group10_Investment_Deflator_Econometrics_Report.pdf](Group10_Investment_Deflator_Econometrics_Report.pdf), not a replacement report or a replication. The PDF is unchanged. Authorship remains **Atabak Nikouseresht, Mahgol Lamei, and Kimia Shokri**.

**Page convention:** “PDF page” means the one-based physical page in a PDF viewer; “printed page” means the footer printed in the report. In this 51-page file the two numbers coincide, including the cover (PDF page 1 / printed page 1). Both are given below so citations remain unambiguous. Embedded screenshots were inspected visually where text extraction omitted tables.

**Status:** Items 1–4 contain confirmed internal inconsistencies or interpretation errors. Item 5 is a confirmed reporting gap: **not independently verifiable does not mean false**. Corrections below describe what the surviving evidence supports; they do not validate integration orders, cointegration, structural identification, causality, forecast performance or every result in the report.

## Confirmed Corrections

### 1. ADF rejection is reversed, and test types are conflated

**Location:** §2.3, “ADF Test Results Summary Table” and “Final Preliminary Assessment,” PDF page 12 / printed page 12; accompanying ADF screenshots on PDF pages 13–14 / printed pages 13–14. Variable definitions appear in §1.1, PDF page 2 / printed page 2.

**Original:** The assessment says the variables are “non-stationary at their levels” and “fail to reject” the unit-root null at 5% and 1%. Yet the table reports, for its rows labelled “Level”:

| Tested label | Reported statistic | Reported p-value |
| --- | ---: | ---: |
| `d_l_DIFL` | -3.77674 | 0.003169 |
| `d_l_dvcft_adjusted` | -3.96712 | 0.001597 |
| `d_l_DMBs` | -7.29280 | 0.000000 |

All p-values printed in that summary table are below 0.01. A displayed `0.000000` is a rounded value, not proof of an exactly zero probability.

**Correct reading:** The ADF null is a unit root; the displayed p-values imply rejection at 1% and 5%, conditional on the associated specification.[1] These labels are already log differences/inflation rates, not the underlying deflator price levels. Rejection for them does **not** establish stationarity of the original price levels.

The summary also mislabels some deterministic specifications as transformations. On PDF page 13 / printed page 13, the `d_l_DIFL` screenshot reports -3.77674 “with constant” and -4.67826 “with constant and trend,” both testing `d_l_DIFL`; the table places the latter under “First Difference.” The import screenshot likewise tests `d_l_DMBS` with constant (-7.2928) and with constant and trend (-7.46396), while the summary calls the second a first-difference test. Actual `d_d_l_...` tests are separately displayed on PDF page 14 / printed page 14. Changing deterministic terms is not first differencing.[1]

**Impact — potentially material to a stated conclusion:** The narrative's justification for further differencing and its later I(1)/cointegration interpretation cannot be accepted from this summary. The table must distinguish the tested series, deterministic terms and lag specification before use.

**Evidence boundary:** This corrects the direction of the reported decisions and specific table/screenshot mismatches, not the underlying data or test execution. No integration order has been re-estimated or certified.

### 2. Recursive ordering is interpreted backwards

**Location:** §3.2, “Chosen Ordering and Justification,” PDF page 19 / printed page 19; “Effect of Ordering on Shock Identification,” PDF page 20 / printed page 20. VAR equation-output screenshots are on PDF pages 21–23 / printed pages 21–23.

**Original:** The stated order is investment-deflator inflation → import inflation → adjusted value-added inflation. Investment inflation is placed first because it supposedly “react[s] immediately to external shocks” from the other two variables. The next page conflates contemporaneous exogeneity with reacting immediately to shocks and describes later variables as responding to preceding variables only through lags.

**Correct reading:** Under the conventional lower-triangular Cholesky impact mapping, the first ordered variable cannot respond contemporaneously to the **identified structural shocks of later equations**. Its own shock can affect all subsequent variables contemporaneously. The second variable can respond on impact to the first shock, and the third can respond on impact to both earlier shocks. Later shocks may affect earlier variables through lagged dynamics.[2]

This is a within-system contemporaneous restriction, not proof of broad macroeconomic exogeneity or immunity to every outside disturbance. The rationale for immediate import/domestic-cost shock effects on investment inflation therefore conflicts with the stated first-position restriction.

**Impact — methodological interpretation issue:** The economic interpretation of orthogonalized IRFs depends on the actual ordering. The displayed VAR screenshots start with import inflation as equation 1 and investment inflation as equation 2, unlike the prose order. Equation listings alone do not prove the ordering used to orthogonalize the IRFs, but this mismatch must be reconciled rather than assuming implementation follows the text.

**Evidence boundary:** The conceptual error is confirmed; the exact IRF shock-identification settings are not recoverable from an original command/session file. No shocks or IRFs were recomputed, and no alternative ordering is endorsed.

### 3. Lag labels and coefficients are attributed inconsistently

**Location:** §4.1, “Key Coefficients,” PDF page 30 / printed page 30; embedded “Model 136” coefficient table on PDF page 33 / printed page 33; “Significant Variables” on PDF page 35 / printed page 35. Related comparison: §4.3, “Long-Run vs. Short-Run Estimates,” PDF page 38 / printed page 38, and embedded regressions on PDF pages 37, 41–42 / printed pages 37, 41–42.

**Original:** Page 35 attaches 0.180561 (p = 0.0444) to `d_l_{dvcft_adj}_2`, prints 0.43380 for lag 3, and calls import lags 1 and 2 significant. Page 30 instead assigns 0.180561 to domestic lag 1 and calls import lag 3 significant.

**Correct reading of the displayed Model 136 table:**

| Row / lag | Coefficient | p-value |
| --- | ---: | ---: |
| Adjusted domestic inflation, lag 1 | 0.180561 | 0.0444 |
| Adjusted domestic inflation, lag 2 | 0.270208 | 0.0018 |
| Adjusted domestic inflation, lag 3 | 0.434380 | 1.84e-05 |
| Import inflation, contemporaneous | 0.0748624 | 0.0054 |
| Import inflation, lag 1 | 0.138246 | 0.0003 |
| Import inflation, lag 3 | 0.0361284 | 0.1687 |
| Import inflation, lag 4 | 0.0261791 | 0.4020 |

There is no import-lag-2 row in that displayed specification. Import lag 3 is not significant at 5%. Thus page 30's domestic lag assignments are supported by this table; the entire earlier paragraph is not erroneous. Page 35's domestic lag-2 attribution and lag-3 numeral, and both pages' import-lag claims, need correction.

The page-38 comparison also mixes coefficient provenance. Its domestic “short-run” value 0.180561 is a particular lag-1 coefficient, not a documented total short-run response. Its import “short-run” value 0.134820 appears in the separate regression screenshots on pages 37 and 41, not in Model 136. The “long-run” values 0.794154 and 0.245583 appear in two separate single-regressor cointegrating-regression screenshots on page 42, for adjusted domestic inflation and import inflation respectively, not as coefficients of one joint specification. They should be labelled with their source specifications; this review does not establish them as ARDL-derived long-run multipliers.

**Impact — local interpretation issue:** Mislabelled lags change the claimed timing and significance of associations. Mixing separate regressions obscures what the short-/long-run comparison actually compares.

**Evidence boundary:** Values above are transcribed from existing screenshots, not newly estimated. The original model-selection process, coefficient transformations and intended comparison are unavailable; no missing lag or multiplier has been reconstructed.

### 4. Johansen signs, normalization and matrix entries are misread

**Location:** §5.1, system description on PDF page 43 / printed page 43; §5.2, “Cointegrating Vectors (Beta)” and “Adjustment Vectors (Alpha),” PDF page 45 / printed page 45; full beta/alpha screenshots on PDF pages 47–48 / printed pages 47–48; rank-test outputs on PDF page 49 / printed page 49.

**Original:** Page 45 gives the normalized beta entries (1, 0, -0.67320), interprets the import coefficient as implying a “decrease in investment deflator inflation,” and treats the domestic zero as evidence of non-significance. It assigns alpha = 1.2202 to adjusted domestic inflation. Page 43 describes a two-variable system, while page 45 lists three variables.

**Correct reading:** Taking the **first displayed vector** under the equilibrium convention `beta' y + deterministic terms = 0`, the coefficient on investment inflation is 1 and that on imports is -0.67320. Moving the import term to the right gives a **positive** 0.67320 import association in the normalized relation, with any deterministic terms retained separately. This is an algebraic interpretation of the printed vector, not a new estimated effect or causal claim.[3]

The screenshot contains **two beta columns**, with the first two rows forming an identity block. The domestic row is 0 in column 1 and 1 in column 2; imports have -0.67320 and -0.71712 respectively. Such normalization zeros identify a basis for the cointegrating space; they do not themselves constitute an exclusion or significance test.[3] Reading the first column alone as evidence that the domestic variable has no long-run role ignores the second column.

The alpha screenshot places 1.2202 in the **investment-inflation row, second column**. The adjusted-domestic row is 0.35762 in column 1 and -0.40062 in column 2. Individual alpha entries must be associated with their equation and vector, not collapsed into one speed per variable. Stability is not established by one alpha sign or magnitude.[3]

**Impact — potentially material to a stated conclusion:** The report's negative-import/substitution interpretation does not follow from its normalized vector. The domestic-exclusion interpretation and alpha attribution also do not follow from the displayed matrices. The two-variable narrative versus three-row/two-column output is an explicit, unreconciled system-description inconsistency.

**Evidence boundary:** Page 49 contains separate three- and two-equation rank-test outputs, including tests beyond rank zero. A rejection of rank zero alone does not establish the fitted rank; the full sequential procedure and matching system must be reconciled.[3] This review does not select a rank or assume the required I(1) interpretation is valid, particularly given item 1. The exact fitted specification and deterministic terms cannot be reliably reconstructed from the narrative and screenshots alone.

## Unverifiable Claims

### 5. PSS bounds-test evidence is incomplete

**Location:** §4.1 prompt on PDF page 30 / printed page 30 requests PSS results. §5.2, “Comparative Analysis with PSS and Engle–Granger,” PDF page 45 / printed page 45, and the summary on PDF page 47 / printed page 47 claim agreement/validation by PSS.

**Original:** “The PSS bounds test strengthens the justification” and agreement supposedly validates the other cointegration findings.

**Correct reporting:** **PSS support is not independently verifiable from the public report.** The narrative and embedded output do not provide an identifiable bounds-test statistic together with the applicable lower/upper critical bounds, significance level and deterministic case. The RESET F-statistic on pages 30 and 34 is a different test, not a published PSS bounds result.

PSS tests the absence of a level relationship using nonstandard F-/t-statistic distributions and bounds for I(0)/I(1) regressors.[5] A checkable record should identify the tested conditional equation, sample, lags, number of level regressors, deterministic specification, integration-order justification within that I(0)/I(1) scope, test statistic, critical-value source and comparison/decision. An F-statistic above the applicable upper bound supports rejection; below the lower bound does not; between the bounds is inconclusive. These requirements cannot be supplied by another diagnostic's p-value.[5]

**Impact — methodological interpretation issue:** The claimed PSS corroboration cannot independently substantiate the report's cointegration, robustness or forecasting statements. It should be presented as an undocumented claim, not as cross-method validation.

**Evidence boundary:** Absence of complete published output does **not** prove the test was never run or that its claimed conclusion is false. No bounds, statistics or missing results have been calculated or imputed.

## What This Errata Does Not Do

Only the public report, current README and surviving public repository history were used for project evidence. They do not reliably separate coauthor analytical contributions. Commit ownership and author metadata were not converted into individual labor claims. Source data, original scripts and saved estimation sessions are absent from the repository, so this review establishes documentary inconsistencies rather than a replication verdict.

No PDF modification, history rewrite, estimation, reconstructed analysis, new result, license or infrastructure change is part of this documentation update.

## Sources

[1] https://www.stata.com/manuals/tsdfuller.pdf — StataCorp, dfuller — Augmented Dickey–Fuller unit-root test, Description and Remarks (pp. 1–3)
[2] https://blog.stata.com/2016/09/20/structural-vector-autoregression-models — David Schenck, Structural vector autoregression models, Stata Blog (20 September 2016), Cholesky identification
[3] https://www.stata.com/manuals/tsvecintro.pdf — StataCorp, vec intro — Introduction to vector error-correction models (pp. 3–4, 7–11): equilibrium, rank selection and Johansen normalization
[5] https://www.repository.cam.ac.uk/bitstreams/3dc112dc-f831-44ae-a3e6-7afaf66c3dbf/download — M. Hashem Pesaran, Yongcheol Shin and Richard J. Smith, Bounds Testing Approaches to the Analysis of Long Run Relationships (February 1999 working paper), abstract, sections 2–3 and critical-value tables
