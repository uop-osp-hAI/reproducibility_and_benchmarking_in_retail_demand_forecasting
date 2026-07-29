LightGBM and Statistical Benchmarks for case study 3/paper-3: Deep learning model using hybrid ATES for modeling and forecasting sales


# Reference: 

* Efat et al. (2024). Deep-learning model using hybrid adaptive trend
estimated series for modelling and forecasting sales.
* Annals of Operations Research*, 339, 297-328.
* https://doi.org/10.1007/s10479-022-04838-6

* **Dataset:** Corporación Favorita (Kaggle), monthly granularity

* **Series:** 162,503 item x store combinations with at least one recorded
transaction in train.csv during 2013-2016. The paper states 4,100 items x
54 stores but applies undisclosed data cleaning ("detecting and discarding
corrupted, incorrect, and incomplete samples", p.304), so the effective
series universe after cleaning is not recoverable.

* **Train:** January 2013 - December 2016

* **Test:** January - August 2017. h=12 is not feasible (Kaggle train.csv ends
15 August 2017, leaving only 8 test months).

* **Horizons:** h=1 (Jan), h=3 (Jan-Mar), h=6 (Jan-Jun) (cumulative evaluation)

* **LGBM model:** Recursive multi-step using a single h=1 model applied
iteratively through the 8 test months. After each monthly prediction the lag
state is updated exactly: lag_1 receives the prediction, lag_k receives the
previous lag_{k-1}, and the rolling statistics are recomputed from the updated
lag vector. Global model across all series, versus the paper's per store design
(54 models). seed=655321.

* **Statistical:** ADI-based classification on DAILY training data :
AutoETS(season_length=1) for smooth demand (ADI<1.32), SBA for
non-smooth (ADI>=1.32)

* **Prerequisites:** Kaggle Corporación Favorita files in 'DATA_DIR':
train.csv, stores.csv, items.csv, holidays_events.csv, oil.csv, transactions.csv
* File name: case_study_3_favorita-grocery-sales-forecasting (download and extract the zipped files and save them to your work environment)
* Link to download from: https://doi.org/10.5281/zenodo.21611057

* Required packages: lightgbm, statsforecast, pandas, numpy, scikit-learn
