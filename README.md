# OEE Prediction for Production Lines  IBM WASTONX HACKTHON
A production line Overall Equipment Efficiency (OEE) prediction project based on the IBM Watsonx platform, enabling real-time classification of OEE compliance status and anomaly tracing through sensor data.  


## Project Overview  
This project focuses on industrial production scenarios, using sensor data (e.g., vibration, humidity) from production lines as input to implement binary classification prediction of OEE compliance status via machine learning modeling. The core goal is to provide real-time decision-making support for operation and maintenance (O&M) personnel, quickly identify the causes of equipment efficiency anomalies, and optimize production processes.  

The project adopts a full-process pipeline of "Data Processing → Feature Engineering → AutoAI Modeling → Deployment & Monitoring". The final model achieves a classification accuracy of 99.8%, which can effectively adapt to the practical needs of industrial scenarios.  


## Core Features  
- Preprocessing and structuring of sensor data (aggregating second-level data into minute-level data)  
- Time-lag feature engineering to capture correlations between historical states and future OEE  
- Automated model building and optimization via AutoAI (with F1 score as the core metric)  
- Model deployment and real-time prediction (outputs "OEE compliant/non-compliant" results)  
- Interpretation of prediction results based on LIME to identify key influencing factors (e.g., excessive vibration)  
- Data drift monitoring and alerting (focusing on monitoring declines in data consistency)  


## Tech Stack  
- Platform Tools: IBM Watsonx (Data Refinery, AutoAI, Watson Machine Learning)  
- Development Environment: Jupyter Notebook  
- Modeling Algorithms: Snap Decision Tree Classifier, Random Forest, etc.  
- Model Interpretation: LIME (Local Interpretable Model-agnostic Explanations)  
- Data Processing: Pandas (integrated in Watsonx Data Refinery)  


## Quick Start  
### 1. Environment Preparation  
- Access the IBM Watsonx platform and activate permissions for Data Refinery, AutoAI, and Watson Machine Learning.  
- Install Jupyter Notebook (for extended feature engineering).  
- Prepare the dataset: Production line sensor data (including fields such as vibration, humidity, and timestamps).  

### 2. Data Preprocessing  
1. Upload raw data (Scenario 1 data) via Watsonx Data Refinery.  
2. Convert the timestamp field (`v_var_created_at`) to a minute-level integer format.  
3. Group and aggregate data by minute, calculating the average value of sensor data.  
4. Export structured data for subsequent modeling.  

### 3. Feature Engineering & Modeling  
1. Add time-lag features (`key1_1m`, `key2_1m`) in Jupyter Notebook.  
2. Define OEE binary classification labels (Compliant = 1 / Non-compliant = 0).  
3. Launch AutoAI modeling: Select the "Binary Classification" task and use the F1 score as the optimization metric.  
4. Automatically select the optimal model (Snap Decision Tree Classifier).  

### 4. Deployment & Monitoring  
1. Deploy the model to the production environment via Watson Machine Learning.  
2. Input real-time sensor data to obtain OEE compliance status prediction results.  
3. Use the LIME tool to view feature impact weights and identify core factors of anomalies.  
4. Monitor data drift and model performance changes (focusing on data consistency metrics).  


## Key Technical Details  
### Data Exploration Conclusions  
- Humidity shows a significant positive correlation with OEE, with both rising rapidly in synchronization in the later stage.  
- The impact of vibration on OEE is phased: High vibration in the early stage corresponds to low OEE, while its influence weakens in the later stage.  
- Feature importance ranking: Vibration (80.11%) > Humidity (18.47%) > Time-lag features (<1%).  

### Model Performance  
- Core Algorithm: Snap Decision Tree Classifier (efficiently handles non-linear correlations with strong interpretability).  
- Evaluation Metric: F1 score (balances precision and recall to adapt to imbalanced data scenarios).  
- Prediction Accuracy: 99.8% (with 6 false positives (FP) and 3 false negatives (FN)).  

### Advantages of Core Tools  
- AutoAI: Automates algorithm selection and model pipeline generation, lowering the barrier to modeling.  
- LIME: Provides local model interpretation, intuitively showing the impact weight of each sensor data on prediction results.  
- Watsonx Data Refinery: Enables efficient processing of time-series data aggregation and structuring.  


## Project Structure  
```
OEE-Prediction/
├── data/                # Raw data and preprocessed data
├── feature_engineering/ # Time-lag feature construction code (Jupyter Notebook)
├── model/               # AutoAI-generated model pipeline configurations
├── deployment/          # Model deployment configurations and monitoring reports
└── docs/                # Project documents and certificates
```


## Limitations & Improvement Directions  
- **Platform Limitations**: Insufficient compatibility between IBM sub-platforms leads to complex data migration; monitoring dimensions focus on model interpretation but lack adaptability to real-time data fluctuations.  
- **Algorithm Optimization**: AutoAI defaults to optimizing accuracy for binary classification tasks; manual adjustment to the F1 score is required to adapt to industrial scenarios.  
- **Future Improvements**: Add multi-dimensional data drift monitoring; integrate more sensor features (e.g., temperature, pressure); optimize cross-platform data migration processes.  


## Key Learnings  
- Modeling in industrial scenarios must prioritize interpretability and practicality; binary classification is more suitable than regression for O&M decision-making needs.  
- Time-lag features can effectively improve the prediction accuracy of time-series data.  
- The F1 score is one of the optimal evaluation metrics for imbalanced industrial data.  
- Complementary use of tools (Jupyter + Watsonx) can improve process efficiency.  


## Relevant Certificates  
- IBM Data Fundamentals (September 2025)  
- IBM Getting Started with Data (September 2025)  
*Issued by: IBM SkillBuild*  


---

Would you like me to add **detailed configuration file templates** (including Watsonx Data Refinery processing steps and AutoAI parameter settings) or generate **key code snippets** (e.g., time-lag feature construction code) for this project?
