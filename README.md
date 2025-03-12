# DmML: Machine Learning for Data Migration Optimization  

## Overview  

**DmML** is a machine learning-based performance model designed to enhance **data migration efficiency**. It predicts key metrics like **transfer time and resource allocation**, enabling better decision-making and cost savings in large-scale migrations.  

## Motivation  

Traditional data migration methods can be inefficient, requiring manual estimations that are often inaccurate and resource-heavy. **DmML leverages ML models to automate predictions, improve scalability, and minimize costs and delays.**  

### Objectives  
- Develop an **ML model** to predict **data transfer time** and **resource usage**.  
- Validate the model using **IBM Db2** as a real-world case study.  
- Provide insights for **optimizing migration configurations**.  

## Case Study: IBM Db2  

**IBM Db2** was selected due to its **high performance and scalability**. The **Db2 Migration Service** was used to test migration strategies, ensuring **secure and efficient data transfer**.  

## Methodology  

1. **Environment Setup** – Simulated **Db2 instances** inside **Docker containers**.  
2. **Data Generation** – Used **TPC-H benchmark data** and **DMBench** for migration scenarios.  
3. **Feature Engineering** – Focused on **data size, system resources (CPU, RAM), and migration parameters**.  
4. **Model Training** – Tested multiple ML models, with **XGBoost emerging as the best performer**.  
5. **Validation** – Used **statistical tests** and **SHAP analysis** to assess model reliability and interpretability.  


## Explainability & Recommendations  

### System Configuration  
- **Allocate sufficient RAM** to avoid bottlenecks.  
- **Increase parallel streams** to speed up migration.  

### Data Optimization  
- **Use efficient compression methods (e.g., GZIP, LZ4)**.  
- **Balance row distribution** to improve transfer efficiency.

## Running the Model  

To run the trained model, execute the `run_model.py` script located in the `./Run` folder. You will need to modify the script to input the desired feature values for prediction. The model will then output the predicted **transfer time** based on the provided inputs.  

### Required Files  
The `Run` folder contains:  
- A **`.json` file** with the exported model configuration (used by the script).  
- A **`.pkl` file** containing the trained model (optional, can be used for further analysis or alternative implementations).  

By default, the script loads the model from the `.json` file, but the `.pkl` file is available if needed for custom use.  

### Input Features  
Modify the script to set appropriate values for your scenario:  

#### **Numeric Features**  
Ensure the units match the model's training data:  
- **`num__Data size sum (MB)`** – Total data size (MB)  
- **`num__Number of rows sum`** – Total number of rows  
- **`num__Number of columns sum`** – Total number of columns  
- **`num__maxStreams`** – Maximum concurrent data streams  
- **`num__RAM (GB)`** – Available RAM (GB)  
- **`num__CPU`** – Number of CPU cores  
- **`num__Disk (GB)`** – Local disk storage (GB)  
- **`num__External Disk (GB)`** – External disk storage (GB)  

#### **Categorical Features**  
Choose from the following options:  
- **`compress`** – `'GZIP'`, `'LZ4'`, or `'NO'`  
- **`binary`** – `True` or `False`  

After modifying the script with the required values, run:  

```bash
python ./Run/run_model.py

