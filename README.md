Model selection for the PDV-ML 2024Q4 version involved iterative testing of different combinations of features and hyperparameters over four accounting periods: 202401, 202402, 202403, and 202404. The objective was to identify the specification that optimized out-of-sample performance, model robustness, and operational consistency. The final model was selected based on superior performance metrics including Median PPE, PPE20, PPE30, WAPE, WPPE, and consistency P90.

The PDV-ML 2024Q4 model architecture consists of two intermediate models (KNN and XGBoost-based AVM Imputation) and one final XGBoost model. This structure was retained from earlier versions due to its proven ability to generalize across diverse housing markets and REO asset types. Each component was tested in parallel, and model selection was guided by performance across both in-sample and out-of-sample data.

The robustness of the model was further validated through K-fold cross-validation and shock testing, both of which confirmed that the selected model is stable and generalizes well across training subsets and scoring periods. The model also meets all business performance benchmarks and regulatory expectations for accounting-based valuation.

4.2.4.1 AI/ML Algorithm Selection
The selected algorithms for PDV-ML 2024Q4 include:

K-Nearest Neighbors (KNN) for deriving local neighborhood-level features such as REO prices, haircut ratios, and price per square foot.

XGBoost (Extreme Gradient Boosting) for both AVM imputation and the final prediction model.

These algorithms were selected for their alignment with the model’s objectives of accurately predicting distressed property values using historical REO data. KNN captures spatial locality, a key factor in real estate, while XGBoost provides robustness to missing data, accommodates nonlinear feature interactions, and performs well under a wide variety of modeling conditions.

The selection is appropriate given the structured tabular nature of the input data, the need for high interpretability (via SHAP values), and the model’s accounting-focused use case. XGBoost is particularly well-suited for scenarios where predictive accuracy and resistance to overfitting are required. Its regularization techniques and ability to handle sparsity make it ideal for production-scale property valuation tasks.

In conclusion, the model selection process—both in terms of architecture and algorithm choice—is well-justified, empirically tested, and aligned with the business need to generate consistent and reliable distressed valuations for REO and CDV inventory.
