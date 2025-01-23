# Predictive Analysis for Manufacturing Operations

## Overview

This project implements a RESTful API for predicting machine downtime or production defects using manufacturing data. It leverages a simple machine learning model and provides endpoints for uploading data, training the model, and making predictions.

## Dataset

The dataset used for this project is sourced from Kaggle: [Optimization of Machine Downtime](https://www.kaggle.com/datasets/srinivasanusuri/optimization-of-machine-downtime?select=Machine+Downtime.csv). It includes key columns such as:
 ```json
   "Hydraulic_Pressure(bar)  Coolant_Pressure(bar)  Air_System_Pressure(bar)  Coolant_Temperature  Hydraulic_Oil_Temperature(?C)  Spindle_Bearing_Temperature(?C)  Spindle_Vibration(?m)  Tool_Vibration(?m)  Spindle_Speed(RPM)  Voltage(volts)  Torque(Nm)  Cutting(kN)  Downtime"
0        160.2                       3.6                       7.4                  42.1                      48.0                             62.0                      0.5                   0.3                4500               220.5        25.3          3.2          1
1        155.8                       3.4                       7.2                  40.5                      46.7                             60.5                      0.4                   0.2                4400               219.8        24.7          3.0          0
 ```
If you encounter issues with accessing the dataset, you can use the included `Machine Downtime.csv` file in this repository.

## Model

For this project, I used a **Logistic Regression** model to predict machine downtime. Logistic Regression is a simple yet effective supervised learning algorithm for binary classification tasks, making it well-suited for our target variable, **Downtime (1: Downtime occurred, 0: No downtime)**.
### Data Preprocessing
To ensure the dataset was clean and ready for modeling, the following preprocessing steps were applied:
- **Handling Missing Values**: Missing values were handled using the dropna method as they were minimal in number. This helped avoid unnecessary imputation and maintained data integrity.<br>
  `data.dropna(inplace=True)`
- **Feature Scaling**: Numerical features were scaled using **MinMaxScaler** to transform them into a range between 0 and 1. This is crucial for Logistic Regression as it ensures that features contribute equally to the model's decision-making process.<br>
  `X_train = scaler.fit_transform(X_train)`
- **Train-Test Split**: The dataset was split into training (70%) and testing (30%) sets to evaluate the model's performance on unseen data.<br>
   `X_train, X_test, y_train, y_test = train_test_split(X_scaled, y, test_size=0.3, random_state=42)`  
  
### Model Optimization
To optimize the model's performance, I employed **GridSearchCV**, a hyperparameter tuning technique that performs an exhaustive search over a specified parameter grid. This ensures the model is trained with the best possible combination of hyperparameters.
### Performance Metrics
To evaluate the model, I used:
- **Accuracy**: Measures the overall correctness of predictions.**model accuracy- 85%**
- **F1-Score**: Balances precision and recall, especially useful for imbalanced datasets.**score- 0.85**
- **Precision**: Proportion of true positive predictions out of all positive predictions.**score- 0.83**
- **Recall**: Proportion of actual positives correctly identified.**score- 0.87**



## Features of the API
The RESTful API is implemented using Flask and includes three main endpoints:

### 1. **Upload Endpoint**
   - **Method**: POST
   - **URL**: `/upload`
   - **Description**: Accepts a CSV file containing manufacturing data and stores it for further processing.
   - **Input**: CSV file with columns (Machine_ID, Coolant_Temperature, Downtime, etc).
   - **Response**:
     ```json
     {
       "columns": [
        "Date",
        "Machine_ID",
        "Assembly_Line_No",
        "Hydraulic_Pressure(bar)",
        "Coolant_Pressure(bar)",
        "Air_System_Pressure(bar)",
        "Coolant_Temperature",
        "Hydraulic_Oil_Temperature(?C)",
        "Spindle_Bearing_Temperature(?C)",
        "Spindle_Vibration(?m)",
        "Tool_Vibration(?m)",
        "Spindle_Speed(RPM)",
        "Voltage(volts)",
        "Torque(Nm)",
        "Cutting(kN)",
        "Downtime"
     ],   
       "message": "File uploaded successfully",
       "status": "success"
     }
     ```

### 2. **Train Endpoint**
   - **Method**: POST
   - **URL**: `/train`
   - **Description**: Trains a machine learning model on the uploaded dataset and returns performance metrics.
   - **Input**: None.
   - **Response**:
     ```json
     {
       "accuracy": 0.85,
       "f1_score": 0.85,
       "precision": 0.83,
       "recall": 0.87,
       "message": "Model trained successfully"
     }
     ```

### 3. **Predict Endpoint**
   - **Method**: POST
   - **URL**: `/predict`
   - **Description**: Accepts JSON input for prediction and returns the prediction with confidence.
   - **Input**: JSON object with keys. e.g.-
     ```json
     {
         "Hydraulic_Pressure(bar)": 125.33,
         "Coolant_Pressure(bar)": 4.936,
         "Air_System_Pressure(bar)": 6.1976,
         "Coolant_Temperature": 35.3,
         "Hydraulic_Oil_Temperature(?C)": 47.8,
         "Spindle_Bearing_Temperature(?C)": 34.6,
         "Spindle_Vibration(?m)": 1.325,
         "Tool_Vibration(?m)": 25.274,
         "Spindle_Speed(RPM)": 19856.0,
         "Voltage(volts)": 368.0,
         "Torque(Nm)": 14.564733,
         "Cutting(kN)": 2.65
     }
     ```
   - **Response**:
     ```json
     {
       "Downtime": "Yes",
       "Confidence": 0.85
     }
     ```


## Technical Requirements

### Frameworks and Libraries
- **Flask**: For building the RESTful API.
- **scikit-learn**: For building the machine learning model.
- **pandas**: For data manipulation.
- **numpy**: For numerical operations.

### Testing Tools
- **Postman**: To test API endpoints.
- **Ngrok**: For exposing the local Flask server to the internet.

---

## File Structure
```
|-- PredictiveAnalysis.ipynb # Colab notebook for Flask API and modeling
|-- Machine Downtime.csv     # Kaggle dataset
|-- README.md                # Project documentation
|-- ModelTraining.ipynb      # File for presenting purpose only (to show how I did data preprocessing and trained my model).
```

---

## Notes for Evaluator
1. Open `PredictiveAnalysis.ipynb` in Google Colab or a Jupyter notebook environment.
2. **Replace NGROK_AUTHTOKEN** in that file with **your own ngrok authtoken** in #Initialize Flask app. The line of code looks like-
   `ngrok.set_auth_token("NGROK_AUTHTOKEN")`
   (Ensure you have a ngrok account. If not, then register on [https://dashboard.ngrok.com/]. Copy your authtoken and do Step 2.
4. Run the cell code (having flask and model).
5. While keep on running, you'll see an URL like <https://5e74-34-21-0-180.ngrok-free.app>. Click on it. If successfully runs, a message "Welcome to Manufacturing API!" will occur. (If not, try Step 2 again. Make sure, your ngrok account is active).
6. Now, copy this URL. Open Postman. Open new request tab and follow these steps-

  #### 1. Upload Request
#### Request: 
   Make a POST request and paste URL with /upload as endpoint. eg- <https://5e74-34-21-0-180.ngrok-free.app/upload> <br>
   Click on Body Tab. Select 'form-data'. Below `Key`, write `File`. <br>
   Select `File` from dropdown list. <br>
   Upload `Machine Downtime.csv` below `Value`.<br>
   Click on `Header` tab. Add `Content-type` - `multipart/form-data`.<br>
   Click Send.<br>
#### Response:
   You'll get Response of "File uploaded successfully!" as mentioned earlier. <br>
   It means file is uploaded successfully.<br>
  #### 2. Train Request
#### Request:
   Make a POST request and paste URL with /train as endpoint. eg- <https://5e74-34-21-0-180.ngrok-free.app/train><br>
   Click on `Header` tab. Add `Content-type` - `application/json`.<br>
   Click Send.<br>
#### Response:
   You'll get response of model accuracy and a message "model trained successfully".<br>
   It means our model is trained on the dataset uploaded and ready to predict.<br>
  #### 3. Predict Request
#### Request:
   Make a POST request and paste URL with /predict as endpoint. eg- <https://5e74-34-21-0-180.ngrok-free.app/predict><br>
   Add `Content-type` - `application/json` in Header tab.<br>
   On Body tab, choose `raw` and select `JSON`.<br>
   Give the input data to predict DOWNTIME or NO DOWNTIME.(eg input format- mentioned earlier).<br>
   Click Send.
#### Response:  
    Result output will display as- "Confidence": 0.82, "Downtime": "Yes".<br>
    
This is how API is including endpoints for basic operations and returning predictions for decision-making.<br>
(I can share my postman collection if your mail is provided).<br>
I hope this project showcases my ability to integrate machine learning and API development effectively. Thank you for evaluating my work!


