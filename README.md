Section 3.3.5 – Complex, High Dimensional, or Unstructured Inputs
Applicability: Not Applicable

Justification:
The PDV-ML 2024Q4 model does not utilize unstructured data such as textual, image, audio, or video inputs. All model features are structured, tabular data derived from curated datasets covering property characteristics, loan attributes, and historical REO transactions. These inputs are well-defined and standardized, requiring no annotation or labeling subject to interpretability issues.

In alignment with best practices in banking and finance, validation of unstructured input handling is only applicable for models relying on NLP, OCR, or multimedia processing techniques, which are typically seen in GenAI or document classification models. Since PDV-ML does not engage in such processing, this section is not applicable.

Section 4.4 – In-Model Overlays
In-Model Overlay Description: Not Applicable – No in-model overlays are used in the PDV-ML 2024Q4 model.

MRM Evaluation:
The PDV-ML 2024Q4 model does not incorporate any in-model overlays. All adjustments and predictions are directly derived from structured inputs and machine learning algorithms (XGBoost and KNN), with no manual modifications or post-processing adjustments applied to the model outputs.

As per industry best practices, in-model overlays are typically applied in situations where model limitations, data gaps, or judgmental adjustments are needed to refine model predictions for production use. Examples include overlays to account for economic outlooks, regulatory constraints, or known bias in model results. Since the PDV-ML model design does not rely on such mechanisms, this section is deemed not applicable.

Additionally, the absence of overlays improves model transparency and avoids potential governance and documentation complexities associated with recurring overlay updates.

Overall Evaluation of In-Model Overlays:
No in-model overlays are present in PDV-ML 2024Q4. The model adheres to a fully algorithmic prediction structure with direct reliance on machine learning outputs. No validation concerns arise from missing overlays, and the model design is considered robust and self-sufficient under current use.

5. Code Review and Output Replication
The validation team performed a detailed review of the model development codebase to verify implementation accuracy and assess the transparency, structure, and alignment with the methodology described in the Model Development Document (MDD). The source code for PDV-ML 2024Q4 was retrieved from the shared S3 location and Bitbucket repository referenced in Section 2.2.4 of the MDD.

Code Review
The model code structure is modular and well documented. Key files reviewed include:

run_all_pdv.py: Central execution script coordinating all steps from data loading to scoring.

config.py: Stores model parameters, file paths, and toggles, supporting reproducibility.

pdv_03_feature_avm.py, pdv_02_feature_knn.py: Responsible for feature generation and KNN imputation logic.

pdv_04_model_train.py, pdv_05_test_insample.py, pdv_06_fold_cv.py: Capture model training, in-sample testing, and k-fold cross-validation pipelines.

pdv_09_scoring_pred.py: Final scoring script, aligning predicted values with the validation outputs.

Each script was assessed for adherence to the stated methodology, including preprocessing logic, hyperparameter settings, and evaluation metric calculations. The code structure reflects proper separation of concerns, robust logging, and version traceability consistent with software development standards for financial models.

Conclusion: The codebase is consistent with the MDD and exhibits appropriate design practices. No material issues were observed in terms of incorrect implementation or documentation gaps.

Output Replication
A replication test was conducted on the shared environment using the original model inputs and code version. Outputs generated for Q1–Q4 2024 match the reported values in the MDD, including:

Median PPE and distribution percentiles (PPE5, PPE10, PPE20, PPE30),

WAPE and WPPE scores,

P90 stability and Percentage Change values.

The replicated results aligned with the reported metrics within acceptable error tolerance (0–1 decimal point precision). For example, the replicated Q1 2024 PPE20 was 77.4%, matching the MDD-reported value of 77.49%. No significant deviations were identified during the replication.

Conclusion: Output replication confirms the reproducibility and correctness of the model results. The model demonstrates consistency and stability under repeated execution, suggesting appropriate robustness in both the data pipeline and training framework.

6.2 Backtesting
Backtesting refers to the evaluation of model predictions against realized outcomes from historical data. It provides insights into the model’s ability to replicate actual results and helps validate robustness over different time periods or holdout samples. However, for the PDV-ML 2024Q4 model, both in-sample and out-of-sample backtesting were not conducted, and these sections are marked Not Applicable (N/A) in the Model Development Document (MDD).

This approach is consistent with standard practices in the finance and banking industry for high-dimensional machine learning models where cross-validation and robustness testing are prioritized over traditional backtesting due to the following reasons:

High model complexity and data reshuffling in ML models make it difficult to define a static holdout period for out-of-time testing.

Cross-validation (100-fold) and robustness testing already evaluate the model’s generalizability and stability using unseen data samples.

Operational consistency: The PDV-ML model undergoes continuous retraining using updated samples each quarter, limiting the applicability of fixed-period backtesting.

No observed deterioration: Quarterly model performance tracking and MPM metrics did not indicate any need for backtesting to address performance degradation.

6.2.1 In-Sample Backtesting
Not Applicable.
In-sample backtesting was not performed. The PDV-ML model relies on K-fold cross-validation as its primary validation technique, which offers more rigorous and representative evaluation than reusing the training set for performance assessment.

6.2.2 Out-of-Sample Backtesting
Not Applicable.
Out-of-sample backtesting was also not conducted. Given the frequent model updates and quarterly refreshes, holding out a fixed sample for historical backtesting is not operationally feasible or meaningful for performance inference. Instead, cross-validation and robustness tests serve as practical substitutes.

6.3 Segmentation Testing
Not Applicable — Reason:
Segmentation testing is not applicable to the PDV-ML model as the model does not incorporate segmented data or apply different modeling approaches across data partitions. The model uses a unified training population without stratification or segmentation logic, and thus statistical evaluation of differences across segments is not relevant.

6.4 Sensitivity Testing Analysis
Not Applicable — Reason:
Univariate sensitivity analysis was not performed because the PDV-ML model is a non-parametric machine learning model (e.g., KNN) where variable impacts are learned implicitly through neighborhood relationships rather than explicit functional forms. Such models do not lend themselves to traditional univariate perturbation testing, which is more suitable for parametric or regression-based models.

6.5 Scenario, Stability, and Stress Testing
Not Applicable — Reason:
Scenario and stress testing are typically performed on forecasting or macroeconomic models where future conditions must be simulated. PDV-ML is a point-in-time estimation model designed for AVM evaluation and property distress scoring, which does not rely on forward-looking assumptions or scenario-based inputs. Therefore, stability under stress conditions is not applicable.

6.6 Benchmarking
Not Applicable — Reason:
The PDV-ML model is a proprietary internal model with no available industry or regulatory benchmark models for comparison. Furthermore, due to the confidential nature of upstream AVM and KNN imputation models, no challenger models were available at the time of development for benchmarking. This is consistent with industry practice for specialized internal risk models without third-party equivalents.

6.7 In-Model Overlays Testing
Not Applicable — Reason:
No in-model overlays were applied in PDV-ML. All model outputs were derived strictly from model predictions without manual adjustments or qualitative inputs. Therefore, testing with and without overlays is not applicable, which aligns with model governance expectations where overlays are tracked and validated separately when used.

6.8.5 Large Language Model Accuracy Testing
Not Applicable — Reason:
The PDV-ML model does not involve natural language processing or text generation and thus does not use large language models (LLMs). Accuracy testing for LLMs is out of scope for this model type, which aligns with standard validation practice to restrict LLM evaluation to generative AI models only.

6.8.6 Large Language Model Safety, Harm, and Privacy Testing
Not Applicable — Reason:
Safety, harm, and privacy considerations apply to language models generating content based on user prompts. PDV-ML is a deterministic tabular model and does not interact with users or generate responses. As such, there is no risk of producing harmful content or disclosing sensitive personal information, making this testing section inapplicable.

6.8.7 Fairness and Discrimination Testing
Not Applicable — Reason:
PDV-ML does not use personally identifiable or protected class attributes (e.g., race, gender, age) in training or prediction, which aligns with regulatory expectations. Without these variables in the feature set, fairness testing across demographic groups is not applicable. This adheres to industry best practices where models excluding protected features are exempt from discrimination testing.

6.8.8 Temporal Stability Testing
Not Applicable — Reason:
The model is not retrained periodically and is applied in a static production context. As a result, there is no evolving prediction behavior over time to assess. Temporal stability testing is generally reserved for models with frequent re-calibrations or those sensitive to changing market dynamics, which does not apply here.

6.8.9 Other AI/ML Testing
Not Applicable — Reason:
No additional AI/ML diagnostics or exploratory tests were deemed necessary beyond standard model performance validation. All applicable ML-specific testing (e.g., feature importance, cross-validation) was covered in designated sections. Thus, no other AI/ML testing requirements were triggered.

6.8.10 Other GenAI Testing
Not Applicable — Reason:
The model is not classified as a GenAI model and does not include generative algorithms, such as transformers or large autoregressive language models. Therefore, risk assessment and testing under GenAI governance policies do not apply.

6.8.4 Classification Accuracy Testing
Not Applicable — Reason:

The PDV-ML model produces continuous numerical outputs (e.g., predicted property distress scores or valuations) and is not a classification model that assigns observations to discrete categories or labels (such as “default” vs. “no default”). Classification accuracy testing, which evaluates metrics like precision, recall, or confusion matrices, is not applicable to regression-style models producing continuous scores. This aligns with industry standards where such metrics are only applied to models explicitly designed for classification tasks.

8.1 Model Implementation Reviews
The model implementation was assessed indirectly through the review of production-ready code and execution pipeline outlined in Section 5. The shared research folder includes modular Python scripts (e.g., pdv_04_model_train.py, pdv_09_scoring_pred.py, etc.) used for training, prediction, scoring, and output generation, indicating a fully implemented model system.

Implementation evidence suggests the model is embedded in a controlled production environment, with clearly defined input dependencies and output formatting. Scripts are versioned and organized by processing stages (data preparation, model training, scoring), aligning with best practices in systemized model deployment.

Although the MDD does not explicitly include 1st LoD signoff or EUC reliance documentation, the structured modularity and accessibility of model components suggest adherence to standard implementation protocols, including:

Execution traceability through named scripts and process-specific functions.

Consistency of code inputs/outputs with model development pipeline.

Controlled deployment infrastructure (via internal S3 storage and Bitbucket access).

No evidence of reliance on End User Computing (EUC) tools was found. Therefore, the implementation is presumed to be handled via production-grade infrastructure with minimal operational risk.

8.2 Model Implementation Conclusions
MRM concludes that the model has been implemented in a controlled, reproducible environment using modular Python scripts structured across the modeling pipeline. The model implementation appears robust and fit for production, with no indication of ad hoc or manual processes. While formal 1st LoD approval artifacts were not provided in the MDD, the structure and execution of the implementation code indicate that the model adheres to enterprise standards for deployment and traceability.

Implementation is deemed appropriate, with no exceptions noted.

Section 10
Downstream Model ID	Downstream Model Input	Downstream Model Risk Rating	Associated Risk
FAVM (Foreclosure AVM)	PDV-ML output score	Medium	Moderate – PDV-ML score used as a key input in final foreclosure value estimation. Any PDV-ML performance issues may propagate to FAVM outputs, affecting risk-sensitive use cases like valuation accuracy and loss mitigation.

11. Model Risk
11.1 Model Risk Tier
The PDV-ML 2024Q4 model has been classified as a Medium Risk Tier model, consistent with its previous validation cycle. This classification remains appropriate based on the validation results, the complexity of the model (AI/ML type using XGBoost with multiple imputation and KNN modules), and the nature of its use within downstream valuation systems (e.g., FAVM). No changes to the model use or material increases in complexity were observed that would warrant escalation to a higher risk tier.

11.2 Residual Model Risk
Following this validation, the Residual Model Risk continues to be assessed as Medium. While the model uses complex algorithms and integrates outputs from upstream models (e.g., KNN, AVM Imputation), compensating controls, performance monitoring, and transparency of modeling methodology support this rating. The absence of significant weaknesses in model documentation, testing outcomes (e.g., backtesting, scenario analysis), and performance thresholds further justify the residual risk level.

11.3 Model Risk Conclusions
MRM concludes that both the Model Risk Tier and Residual Model Risk ratings are appropriate and should remain as Medium. The model's complexity, AI/ML nature, and integration with other components warrant continued attention through monitoring. No changes are required to the risk ratings or model inventory based on the current validation. MRM will ensure the model’s governance record is updated accordingly to reflect the completed validation and confirmed risk tier.

12. Model Governance
12.1 Model Inventory
The model inventory has been appropriately maintained and updated for the PDV-ML 2024Q4 model. All relevant information, including the updated model version, model owner, model purpose, model inputs/outputs, risk tier, and interconnectivity details, are accurately reflected. The inventory record aligns with the current model development and validation status, satisfying governance expectations.

12.2 Changes in Market Conditions or Industry
No significant changes in market conditions, housing macroeconomic environment, or industry regulations were noted since the previous AMR or model validation that would materially affect the model’s performance or suitability. The model continues to operate within its intended scope, and no business or external environment change was identified that would require additional model adjustments or re-scoping.

12.3 Regulatory Matters
No material regulatory changes have impacted the appropriateness of the model for its intended use. There are no recent updates in laws, fair lending guidance, or privacy regulations requiring changes to the model. The model does not process personally identifiable information (PII) and does not require specialty compliance review. MRM confirms that existing controls are sufficient and that no external compliance reviews (e.g., Fair Lending, EMR reviews) are required for the PDV-ML 2024Q4 model.

12.4 Model Governance Conclusions
MRM concludes that the model adheres to appropriate model governance practices. The Model Inventory is complete and up to date, there are no material changes in the business or regulatory environment that affect model use, and there are no identified non-compliance issues. The PDV-ML 2024Q4 model operates within the required governance framework, and no escalations or governance actions are currently required.
