7. Model Limitations and Compensating Controls
This section evaluates the limitations identified in the MDD and MRM review, including their root causes and the adequacy of compensating controls, monitoring, and communications to model users.

7.1 Model Limitations Identified by Model Owner
The PDV-ML 2024Q4 model, a medium-risk AI/ML valuation model, has the following limitations noted by the Model Owner:

Known Limitations:

The model is designed primarily for distressed property valuation and may not generalize well to regular market conditions.

AVM values are imputed using an intermediate XGBoost-based AVM Imputation model when not available, which introduces additional modeling layers and potential propagation of error.

KNN neighborhood variables depend on assumptions around spatial similarity, which may break down in highly heterogeneous locations.

Extrapolation logic was removed in this version for simplicity, which may limit short-term prediction responsiveness.

Situational Limitations:

The model’s predictions may not be suitable in extreme macroeconomic volatility or when offer data availability drops significantly.

The model is not designed for applications requiring counterfactual predictions (e.g., what-if simulations of pricing under policy shifts).

7.2 Impact of Model Limitations
The primary impact of these limitations is on model generalizability and stability under rare or extreme market conditions. However, the 2024Q4 version shows strong performance metrics (e.g., PPE20 > 77%, WAPE < 12%, P90 < 11%) under normal operational conditions.

Quantitatively:

The removal of extrapolation reduced WPPE variance without degrading accuracy.

Imputation of AVM values has been validated via XGBoost robustness and excludes deprecated features like cscore_r.

These limitations are well-documented, and their impact is contained through strong internal model design and monitoring.

7.3 Compensating Controls Applied to Model Limitations
Compensating controls applied include:

Use of robustness testing across four consecutive quarters and under 5% sample shocks.

Monthly cross-validation using 100-fold testing to monitor performance drift.

Hard-coded extrapolation bounds (e.g., adj_factor bounded between 0.85 and 1.15) to prevent undue volatility from trend adjustments.

Routine retraining with extended data (36 months vs. prior 26 months) to ensure sample diversity.

These controls mitigate most operational risks associated with the model limitations.

7.4 Model Limitations Identified by MRM
MRM independently identified the following:

Root Cause: Model dependence on AVM imputations and KNN-based neighborhood metrics introduces assumptions on data availability and comparability.

Risk: If AVM inputs or REO sales data become unreliable, model accuracy could deteriorate, particularly for rare property types.

Impact: Degradation in precision and interpretability, especially when extrapolated to niche asset types or regions with low density of REO transactions.

MRM Required Control: Maintain quarterly validation cadence and retraining cycles, as well as stability monitoring using P90 and WPPE.

7.5 Usage Limitations
The model is not to be used for:

Properties with insufficient historical data (e.g., newly developed areas).

Use cases involving regular-condition pricing, since the model is calibrated on distressed assets.

Macro-stress scenario modeling or capital planning.

These limitations are communicated clearly in the MDD and usage guidance.

7.6 Model Limitations and Compensating Controls Conclusions
Overall, the PDV-ML 2024Q4 model has clearly defined and well-managed limitations. Adequate compensating controls are in place through robustness testing, performance monitoring, and retraining. Limitations are communicated to users and are not expected to materially impair the model’s ability to serve its intended purpose. No further MRM remediation actions are necessary at this time.

9. Model Performance Monitoring (MPM)
9.1 MPM Design
The MPM Plan for the PDV-ML 2024Q4 model is well-designed and adheres to the requirements outlined in the Model Use and Monitoring Standard. The plan outlines clear performance metrics (Median PPE, PPE20, PPE30, WAPE, WPPE, and P90) and includes rationale for threshold selection. Monitoring is scheduled quarterly, aligning with the model’s scoring cadence.

9.2 MPM Adherence
The model adheres to the MPM Plan as designed. Metrics and thresholds are consistently monitored across each scoring cycle (202401–202404), and reports are well-documented. No benchmark or challenger models are used, which is appropriate for this use case. The MPM results are based on REO data and follow the execution frequency defined in the plan.

9.3 MPM Threshold Breaches
No material threshold breaches were observed in the past year. For PDV-ML 2024Q4, the model maintained:

PPE20 > 75%

WAPE < 20%

PPE30 < 20%

P90 < 18%

In all quarters, metrics were comfortably within thresholds. For example, Q1–Q4 P90 values remained under 11%, and WAPE ranged between 10.86 and 16.73. No escalation procedures were triggered.

9.4 MPM Outcome Analysis
MPM results do not indicate any material deterioration in model performance. There are no consistent upward trends in WAPE or PPE30, and P90 decreased significantly relative to prior production versions. Stability testing across quarters confirms robustness. Therefore, no revision in methodology or assumptions is warranted.

9.5 MPM Conclusions
The MPM Plan is appropriately designed and effectively implemented. Results confirm continued strong performance of the model in terms of accuracy and stability. No material breaches or deviations were observed. The model is considered fit-for-use, with no adjustments or escalations required.

10. Model Interconnectivity
The PDV-ML 2024Q4 model integrates outputs from two upstream models:

Upstream Model ID	Upstream Model Output	Upstream Model Risk Rating	Associated Risk
KNN (Neighborhood Stats)	Neighborhood-level REO price, haircut, and Ft/Sq	Medium	Low – Used for feature generation only
AVM Imputation Model	Imputed AVM values	Medium	Moderate – Inputs fed into final model via XGBoost pipeline

The model appropriately manages risk from these upstream dependencies. All dependencies are internal models with established controls and version management. No objections were noted from upstream model owners. No downstream dependencies are identified for PDV-ML, which limits propagation risk.
