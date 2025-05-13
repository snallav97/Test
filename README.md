6. Model Development Evidence
This section evaluates the model’s development and testing process. All testing was performed by the 1st Line of Defense (LoD), reviewed by MRM, and aligns with documentation provided in the MDD. Independent testing by MRM was not required due to satisfactory LoD execution.

6.1 Technical Assumptions Analysis
i. Key Technical Assumptions
The PDV-ML model is based on machine learning algorithms (KNN and XGBoost) which do not assume functional forms between predictors and target variables. Assumptions primarily relate to the stability of training data, consistent feature availability, and target distribution (REO prices). The following assumptions were documented and tested:

Key Technical Assumption	MRM Evaluation
Consistency of AVM imputation via XGBoost	Tested across time. Performance stable.
Neighborhood-level features from KNN (location only)	Verified. No material sensitivity to distance k.
Training window stability (36 months)	Reasonable. Supported by robustness test results.

ii. Non-Key Technical Assumptions

Non-Key Technical Assumption	MRM Evaluation
Random seed ensemble reduces prediction volatility	Verified. STD and P90 metrics demonstrate gains.

iii. Technical Assumptions Identified by MRM
None identified.

6.2 Backtesting
i. In-Sample Backtesting
Not performed. Model evaluation uses out-of-sample quarterly performance and comparison to the prior production model (2021Q3).

ii. Out-of-Sample Backtesting
Out-of-sample testing was performed using REO data from 202401 to 202404. Results compared PDV-ML 2024Q4 against the current production model. Metrics used include Median PPE, PPE20, PPE30, WAPE, and WPPE. The new model consistently outperformed the previous version, demonstrating:

PPE20 increase > 20%

PPE30 decrease > 20%

WAPE < 12%

P90 (prediction shift across months) < 11%

6.3 Segmentation Testing
Not Applicable.
The model does not use population or business segmentation. All properties are scored uniformly based on available data.

6.5 Scenario, Stability, and Stress Testing
Not Applicable.
No formal scenario or stress testing is conducted. However, robustness testing across different training and scoring periods (202401–202404) serves as a proxy to assess model stability under varying data availability.

6.8 Testing Details (only applicable sections completed below)
i. Cross Validation Testing
100-fold K-cross-validation was used to simulate training-validation splits. The 2024Q4 model showed consistent performance across folds and months. The median PPE remained < 1.4 and WAPE < 12%. The WPPE metric remained close to zero, indicating prediction bias is well controlled. K=100 was selected for computational efficiency and generalizability.

ii. Feature Importance Testing
SHAP values were used to evaluate feature importance across training datasets. Top contributing features include REO haircut, REO per square foot, engineered loan/property features, and imputed AVM. Features were interpretable and aligned with domain expectations.

iii. Robustness Testing
Model robustness was tested by randomly removing 5% of the training data (shock test). The resulting model produced similar output, with < 3% change in median PPE and < 7% shift at the 90th percentile. This validates model stability across small sampling shocks.

All other testing types were marked as “Not Applicable” in the MDD:

Classification Accuracy Testing

Fairness and Discrimination Testing

Temporal Stability Testing

Other AI/ML Testing

Other GenAI Testing (not a GenAI model)

6.9 Model Development Evidence Conclusions
The PDV-ML 2024Q4 model meets all documented technical and performance-related expectations. All key assumptions were appropriately validated through quantitative testing. The model demonstrated strong performance improvements over the existing version, and no additional assumptions, overlays, or stress mechanisms were required. Model evidence supports approval for business use.

Let me know if you want this transferred to your validation report document or if you're ready to proceed to Section 7: Outcome Analysis.








