LightGBM and Statistical Benchmark models for Andrade & Cunha paper on disaggregated XGB (2023)

# Reference:
* Andrade & Cunha (2023). Disaggregated retail demand forecasting:A gradient boosting approach
*  https://doi.org/10.1016/j.asoc.2023.110283

* Dataset:    Corporación Favorita (Kaggle), weekly granularity
* Series:     1,623 items × 54 stores (items used in the paper's pipeline)
* Train:      All weeks before the final 8 weeks (start date varies per store)
* Test:       Last 8 weeks : June 25 to August 13 2017
* Evaluation: h=1 through h=8 weekly horizons

# LGBM model: Per-store models (54 models) matching the paper's XGBoost design
* Uses the paper's precomputed lagged_features_2.csv feature set
* seed=42 added for reproducibility (paper's code has no seed)
* Statistical: SBC at weekly granularity. AutoETS(season_length=52) captures the annual seasonal cycle.

# Prerequisites:
Run the paper's Articles 1–5  from the paper's repository (CodeOcean capsule 3786508) to generate the following files:
* calculated_features/lagged_features_2.csv
* calculated_features/product_features.csv
* calculated_features/store_features.csv
* calculated_features/seasonal_features.csv
* calculated_features/features/calendar_features.csv

# Required packages: lightgbm, statsforecast, pandas, numpy, scikit-learn
* do a pip install lightgbm statsforecast pandas numpy scikit-learn

  # Instructions to run the notebooks in the following order:
  
  For preparing the data: (from the paper's pipeline)
  1. First notebook to run: Case_Study_1_data_prep_notebook1_Article_1_EDA
  2. Second notebook to run: Case_Study_1_data_prep_notebook2_Article_2_FillDates
  3. Third notebook to run: Case_Study_1_data_prep_notebook3_Article_3_StockoutIdentification
  4. Fourth notebook to run : Case_Study_1_data_prep_notebook4_Article_4_GroupWeekly
  5. Fifth notebook to run: Case_Study_1_data_prep_notebook5_Article_5_FeatureEngineering
     
  Our Statistical and ML benchmark:
  6. Case_Study_1_Disaggregated_Retail_demand_forecasting_Gradient_Boosting_statistical_and_ML_benchmarks

OR

If you want to altogether skip the data preparation steps and run only the benchmarking notebook, download the following zipped folder, extract files and save them to your input directory
* File name: case_study_1_calculated_features
* Link to download from: https://zenodo.org/uploads/21611057

  Ensure to change the paths in the notebooks as needed.
  
