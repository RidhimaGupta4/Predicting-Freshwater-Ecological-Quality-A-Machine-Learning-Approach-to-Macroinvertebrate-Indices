# Macroinvertebrate Abundance Trends in England’s Rivers (1990–2024)

## 📌 Project Overview
This project delivers a production-ready statistical framework for assessing national macroinvertebrate trends using 30+ years of Environment Agency (EA) open data[cite: 13, 14, 90]. The primary challenge addressed is **measurement heterogeneity**: reconciling legacy categorical placeholders (e.g., AB indices) with modern numeric counts and sub-sampled data[cite: 19, 21, 94, 101].

By implementing **Seasonal Censored-Normal Generalized Additive Models (CNORM GAMMs)**, this pipeline produces season-aware national indicators that respect interval uncertainty and phenology[cite: 115, 590, 931].

## 🛠️ Technical Stack
* **Language:** R [cite: 136]
* **Modeling:** `mgcv` (Censored GAMMs with REML smoothing) [cite: 546, 616]
* **Data Engineering:** Apache Arrow (for high-performance Parquet processing) [cite: 274, 866]
* **Visualization:** `ggplot2`, `gratia` [cite: 958][cite_start], and `sf` for spatial mapping [cite: 243]

## 🔬 Key Statistical Features
* **Interval-Censored Likelihood:** Every observation is treated as an interval $[L_i, U_i]$ on a variance-stabilizing $\sqrt{\cdot}$ scale to account for one-significant-figure rounding and categorical bins[cite: 114, 591, 851].
* **Seasonal Phenology:** Separate thin-plate regression splines for Spring and Autumn to capture divergent life-cycle dynamics[cite: 554, 615, 853].
* **Precision Weighting:** Implemented $w_i \propto 1 / (width_i + 1)$ to ensure exact counts carry more statistical weight than broad categorical ranges[cite: 248, 566, 639].
* **Spatial Heterogeneity:** Integrated site-level random intercepts to produce site-marginal national curves, ensuring trends reflect population-level change rather than site-specific noise[cite: 557, 854, 863].
* **Model Triangulation:** Validated findings across four aligned models: Presence/Absence (Binomial), Ordered Categorical (OCAT), Censored-Poisson, and the headline CNORM[cite: 118, 543, 855].

## 📊 Findings Summary
Across five focal families (*Aphelocheiridae, Brachycentridae, Cordulegastridae, Odontoceridae, Potamanthidae*), the analysis reveals a characteristic "dip and recovery"[cite: 34, 121, 912]:
* **General Trend:** Significant national increase through the 1990s to a mid-2000s peak, followed by stabilization and a recent recovery into the 2020s[cite: 652, 729, 912].
* **Spatial Insight:** For the *Aphelocheiridae* family, approximately 97% of studied sites showed positive abundance shifts between the early ($\le2005$) and recent ($\ge2006$) windows[cite: 1897].

## 📂 Repository Structure
* `/data_preprocessing`: Scripts for Arrow-based ingestion and interval construction logic[cite: 277].
* `/models`: R implementation of the CNORM, OCAT, and PA GAMMs[cite: 543].
* `/viz`: Code for generating "Rounding Fingerprints," seasonal trajectories, and BNG-projected change maps[cite: 119].
