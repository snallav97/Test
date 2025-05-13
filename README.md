4. Conceptual Soundness
4.1 Model Methodology
i. Model Methodology

The PDV-ML 2024Q4 model is a machine learning-based model designed to estimate distressed property values using REO transaction data. It incorporates two intermediate models—KNN for localized neighborhood features and XGBoost for AVM imputation—feeding into a final XGBoost valuation model. This modular design enhances predictive performance by combining spatial sensitivity with imputation robustness.

The model's design reflects best practices in the property valuation domain, combining market-driven assumptions with automation and repeatability. It avoids subjective expert opinion by relying on historical REO transactions and engineered features, aligning with Fannie Mae's business need for consistent and reliable accounting valuation of REO and CDV inventory. The structure also supports quarterly retraining and aligns with industry standards in predictive modeling, ensuring adequate mathematical rigor and computational efficiency.

ii. Consistency of Model Methodology with Academic Literature and Industry Practice

The methodology is consistent with established academic and applied practices. The use of KNN for spatial proximity analysis and XGBoost for imputation and valuation is well-supported in real estate price modeling literature. The modeling techniques are widely used in both academia and industry for regression tasks involving large datasets with missing values and nonlinear relationships.

iii. Consideration of Alternate Methodologies

Traditional valuation methods such as sales comparison, cost approach, and income approach were considered conceptually, but were not selected due to their reliance on expert judgment, limited automation, and potential inconsistency across assets. The PDV-ML 2024Q4 model was preferred for its ability to generalize from past REO data, automate valuation at scale, and support repeatable accounting exercises. The selected machine learning structure balances model complexity, explainability, and predictive performance.

iv. Model Retraining

The retraining process for PDV-ML 2024Q4 includes updates to sample size (increased to 36 months), hyperparameter tuning (e.g., XGBoost objective changed from reg:gamma to reg:squarederror), and feature expansion. Retraining is triggered by defined criteria including changes in data availability and performance degradation. The acceptance criteria for the recalibrated model include PPE20 improvement ≥3%, WAPE <20%, PPE30 reduction ≥3%, and P90 <18%. All criteria were met, validating the retraining cadence and methodology.

4.2 Model Specification
i. Model Estimation Technique

The model employs XGBoost regression as the main estimation method, using engineered and imputed features from intermediate KNN and AVM models. Relationships among variables are captured via tree-based boosting, which inherently models nonlinearities and interactions. XGBoost was chosen for its robustness, scalability, and effectiveness on large, sparse datasets common in distressed asset modeling.

ii. Model Segmentation

The model does not implement segmentation. Instead, it treats the entire U.S. REO/CDV population as a single modeling market. This approach is justified given the accounting use case and the need for nationwide consistency. Business rationale supports this decision to ensure that the same model logic is applied across the book of business without introducing segmentation-induced volatility.

iii. Variable Selection Process

Initial variable selection was based on domain relevance and feature engineering. A total of 58 features from PDV-ML 1.0 were reduced to 26 in PDV-ML 2024Q4 using a combination of SHAP value importance, WAPE contribution, and overfitting analysis. Feature inclusion/exclusion decisions were driven by iterative testing and performance trade-offs, ensuring retained variables were both predictive and stable.

4.3 Business Assumptions
i. Key Business Assumptions

Key Business Assumption	MRM Evaluation
REO data from non-Fannie Mae properties can be used to model Fannie Mae REO values	Reasonable, given market-driven pricing
Cash offers do not affect REO values	Acceptable—REO market operates independently of cash offer presence
REO offer price reflects final sales price	Valid—use of offer price as proxy for final value is supported by data review

All assumptions were reviewed and found to be consistent with market behavior and appropriately documented.

ii. Non-Key Business Assumptions

Non-Key Business Assumption	MRM Evaluation
PDV-ML model can only be applied to primary loans within the U.S.	Aligned with intended use
Model values are limited to accounting purposes, not lending decisions	Clearly communicated

iii. Business Assumptions Identified by MRM

MRM Identified Key Business Assumptions	MRM Evaluation
None	N/A

4.4 In-Model Overlays
In-Model Overlay Description	MRM Evaluation
N/A	Overlays are not applicable to this model

Overall Evaluation of In-Model Overlays
No overlays are used in the PDV-ML 2024Q4 model, which simplifies governance and enhances transparency.

4.5 AI/ML Model Refinement
Refinements for the PDV-ML 2024Q4 model include hyperparameter tuning, removal of weak features, and the elimination of the trend adjustment mechanism (set to neutral bounds). These updates were driven by performance monitoring and did not involve a change in methodology. No alternate AI/ML refinements were applied.

4.6 Conceptual Soundness Conclusions
The PDV-ML 2024Q4 model demonstrates strong conceptual soundness. The methodology is aligned with industry practice and academic standards, the model structure is modular and rigorous, and the business assumptions are well-supported. The validation results confirm that the model meets precision, accuracy, and robustness criteria appropriate for its use case in distressed asset valuation for accounting purposes.

