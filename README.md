# Predictive Analysis for Manufacturing Operations API

## Overview

This project implements a RESTful API for predicting machine downtime or production defects using manufacturing data. It leverages a simple machine learning model and provides endpoints for uploading data, training the model, and making predictions.

## Dataset

The API uses synthetically generated manufacturing data, including features like Machine_ID, Temperature, Run_Time, and Downtime_Flag. This was chosen due to the unavailability of suitable public datasets for the specific use case.

## Model

A Decision Tree Classifier (or another suitable model you used) is employed for prediction. The model is trained on the uploaded or provided data and evaluated using metrics like accuracy and F1-score.

## API Endpoints

The API exposes the following endpoints:

- */upload (POST):* Accepts a CSV file containing manufacturing data. Returns a success message upon successful upload.
- */train (POST):* Trains the model on the uploaded dataset and returns performance metrics (accuracy, F1-score).
- */predict (POST):* Accepts JSON input (e.g., {"Temperature": 80, "Run_Time": 120}) and returns the prediction (e.g., {"Downtime": "Yes", "Confidence": 0.85}).

## Technical Details

- *Language:* Python
- *Framework:* Flask
- *Machine Learning Library:* scikit-learn

## Setup and Usage

1. *Clone the repository:* git clone <repository_url>
2. *Install dependencies:* pip install -r requirements.txt
3. *Replace authtoken:* Replace NGROK_AUTHTOKEN in the app.py file with your own ngrok authtoken (if used).
4. *Run the API:* python app.py
5. *Access the API:* The API will be accessible at http://127.0.0.1:5000/.

## Example Requests and Responses

*Upload:*
Use code with caution
POST /upload Content-Type: multipart/form-data

Upload a CSV file named 'manufacturing_data.csv'
 
*Response:*
Use code with caution
json { "message": "Data uploaded successfully" }

 
*Train:*
Use code with caution
POST /train Content-Type: application/json

 
*Response:*
Use code with caution
json { "message": "Model trained successfully", "accuracy": 0.95, "f1_score": 0.92 }

 
*Predict:*
Use code with caution
POST /predict Content-Type: application/json

{ "Temperature": 80, "Run_Time": 120 }

 
*Response:*
Use code with caution
json { "Downtime": "Yes", "Confidence": 0.85 }

 
## Notes

- Ensure you have a working ngrok installation and account if you plan to use it for public access.
- The synthetic dataset used for this project is generated for demonstration purposes and may not perfectly reflect real-world manufacturing data.


## Contributing

Feel free to contribute to this project by opening issues or submitting pull requests.

## License

This project is licensed under the MIT License.
Use code with caution
Remember to replace the placeholders like <repository_url> and the example accuracy/F1-score values with your actual details.

This comprehensive README file provides a good overview of your project, how to set it up, use the API, and understand its functionality. It should help the evaluator easily assess your work.



# Predictive Analysis for Manufacturing Operations

## Objective
This project demonstrates predictive analysis on manufacturing data, focusing on predicting machine downtime or production defects using a RESTful API. The API allows uploading data, training a predictive model, and making real-time predictions.

---

## Dataset
The dataset used is `Machine Downtime.csv`, which includes the following key columns:
- **Machine_ID**: Unique identifier for each machine.
- **Temperature**: Machine temperature in degrees.
- **Run_Time**: Time the machine has been running in hours.
- **Downtime_Flag**: Binary flag indicating downtime (1: Yes, 0: No).

You can use this dataset or replace it with a similar manufacturing-related dataset.

---

## Features of the API
The RESTful API is implemented using Flask and includes three main endpoints:

### 1. **Upload Endpoint**
   - **Method**: POST
   - **URL**: `/upload`
   - **Description**: Accepts a CSV file containing manufacturing data and stores it for further processing.
   - **Input**: CSV file with columns (Machine_ID, Temperature, Run_Time, Downtime_Flag).
   - **Response**:
     ```json
     {
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
       "accuracy": 0.92,
       "f1_score": 0.89,
       "message": "Model trained successfully"
     }
     ```

### 3. **Predict Endpoint**
   - **Method**: POST
   - **URL**: `/predict`
   - **Description**: Accepts JSON input for prediction and returns the prediction with confidence.
   - **Input**: JSON object with keys (e.g., {"Temperature": 80, "Run_Time": 120}).
   - **Response**:
     ```json
     {
       "Downtime": "Yes",
       "Confidence": 0.85
     }
     ```

---

## Technical Requirements

### Frameworks and Libraries
- **Flask**: For building the RESTful API.
- **scikit-learn**: For building the machine learning model.
- **pandas**: For data manipulation.
- **numpy**: For numerical operations.

### Testing Tools
- **Postman**: To test API endpoints.
- **Ngrok**: For exposing the local Flask server to the internet (if needed).

---

## Setup Instructions

### 1. Install Dependencies
Ensure you have the required Python packages. Install them using the following command:
```bash
pip install -r requirements.txt
```

### 2. Run the API Locally
Open the provided Colab notebook (`PredictiveAnalysis.ipynb`) and run all cells to:
- Implement the Flask app.
- Train the model.
- Test the API.

### 3. Test API Endpoints
Use Postman or cURL to test the following endpoints:
- **Upload Endpoint**: Send a POST request to `/upload` with `Machine Downtime.csv`.
- **Train Endpoint**: Send a POST request to `/train`.
- **Predict Endpoint**: Send a POST request to `/predict` with JSON input (e.g., {"Temperature": 80, "Run_Time": 120}).

### 4. Expose API Using Ngrok (Optional)
To make the API publicly accessible:
```bash
ngrok http 5000
```
This will provide a public URL (e.g., `https://<ngrok_url>.ngrok.io`) to test the API.

---

## Data Modeling

### Model Selection
- **Logistic Regression**: Chosen for its simplicity and interpretability for binary classification tasks.

### Performance Metrics
- **Accuracy**: Measures the overall correctness of predictions.
- **F1-Score**: Balances precision and recall, especially useful for imbalanced datasets.

---

## Example API Requests and Responses

### 1. **Upload Request**
#### Request:
```bash
POST /upload
Content-Type: multipart/form-data
File: Machine Downtime.csv
```
#### Response:
```json
{
  "message": "File uploaded successfully",
  "status": "success"
}
```

### 2. **Train Request**
#### Request:
```bash
POST /train
```
#### Response:
```json
{
  "accuracy": 0.92,
  "f1_score": 0.89,
  "message": "Model trained successfully"
}
```

### 3. **Predict Request**
#### Request:
```bash
POST /predict
Content-Type: application/json
{
  "Temperature": 75,
  "Run_Time": 100
}
```
#### Response:
```json
{
  "Downtime": "No",
  "Confidence": 0.95
}
```

---

## File Structure
```
|-- PredictiveAnalysis.ipynb # Colab notebook for Flask API and modeling
|-- Machine Downtime.csv     # Sample dataset
|-- README.md                # Project documentation
```

---

## Notes for Evaluator
1. Open `PredictiveAnalysis.ipynb` in Google Colab or a Jupyter notebook environment.
2. Follow the cell instructions to deploy and test the API.
3. Modify API configuration as needed (e.g., port number or public URL).



# Predictive Analysis for Manufacturing Operations

## Objective
This project demonstrates predictive analysis on manufacturing data, focusing on predicting machine downtime or production defects using a RESTful API. The API allows uploading data, training a predictive model, and making real-time predictions.

---

## Dataset
The dataset used is `Machine Downtime.csv`, which includes the following key columns:
- **Machine_ID**: Unique identifier for each machine.
- **Temperature**: Machine temperature in degrees.
- **Run_Time**: Time the machine has been running in hours.
- **Downtime_Flag**: Binary flag indicating downtime (1: Yes, 0: No).

This dataset serves as the basis for training the model and testing predictions. You can use this or replace it with a similar manufacturing-related dataset.

---

## Features of the API
This RESTful API is my attempt to create a simple, functional tool for predictive analysis. It includes three main endpoints:

### 1. **Upload Endpoint**
   - **Method**: POST
   - **URL**: `/upload`
   - **Description**: Accepts a CSV file containing manufacturing data and stores it for further processing.
   - **Input**: CSV file with columns (Machine_ID, Temperature, Run_Time, Downtime_Flag).
   - **Response**:
     ```json
     {
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
       "accuracy": 0.92,
       "f1_score": 0.89,
       "message": "Model trained successfully"
     }
     ```

### 3. **Predict Endpoint**
   - **Method**: POST
   - **URL**: `/predict`
   - **Description**: Accepts JSON input for prediction and returns the prediction with confidence.
   - **Input**: JSON object with keys (e.g., {"Temperature": 80, "Run_Time": 120}).
   - **Response**:
     ```json
     {
       "Downtime": "Yes",
       "Confidence": 0.85
     }
     ```

---

## Technical Requirements

### Frameworks and Libraries
I used the following technologies to develop this project:
- **Flask**: For building the RESTful API.
- **scikit-learn**: For building the machine learning model.
- **pandas**: For data manipulation.
- **numpy**: For numerical operations.

### Testing Tools
- **Postman**: To test API endpoints.
- **Ngrok**: For exposing the local Flask server to the internet (if needed).

---

## Setup Instructions

### 1. Install Dependencies
Ensure you have the required Python packages. Install them using the following command:
```bash
pip install -r requirements.txt
```

### 2. Run the API Locally
Open the provided Colab notebook (`PredictiveAnalysis.ipynb`) and run all cells to:
- Implement the Flask app.
- Train the model.
- Test the API.

### 3. Test API Endpoints
I recommend using Postman or cURL to test the following endpoints:
- **Upload Endpoint**: Send a POST request to `/upload` with `Machine Downtime.csv`.
- **Train Endpoint**: Send a POST request to `/train`.
- **Predict Endpoint**: Send a POST request to `/predict` with JSON input (e.g., {"Temperature": 80, "Run_Time": 120}).

### 4. Expose API Using Ngrok (Optional)
To make the API publicly accessible:
```bash
ngrok http 5000
```
This will provide a public URL (e.g., `https://<ngrok_url>.ngrok.io`) to test the API.

---

## Data Modeling

### Model Selection
I chose **Logistic Regression** for its simplicity and interpretability for binary classification tasks. It fits well with the nature of this project.

### Performance Metrics
To evaluate the model, I used:
- **Accuracy**: Measures the overall correctness of predictions.
- **F1-Score**: Balances precision and recall, especially useful for imbalanced datasets.

---

## Example API Requests and Responses

### 1. **Upload Request**
#### Request:
```bash
POST /upload
Content-Type: multipart/form-data
File: Machine Downtime.csv
```
#### Response:
```json
{
  "message": "File uploaded successfully",
  "status": "success"
}
```

### 2. **Train Request**
#### Request:
```bash
POST /train
```
#### Response:
```json
{
  "accuracy": 0.92,
  "f1_score": 0.89,
  "message": "Model trained successfully"
}
```

### 3. **Predict Request**
#### Request:
```bash
POST /predict
Content-Type: application/json
{
  "Temperature": 75,
  "Run_Time": 100
}
```
#### Response:
```json
{
  "Downtime": "No",
  "Confidence": 0.95
}
```

---

## File Structure
```
|-- PredictiveAnalysis.ipynb # Colab notebook for Flask API and modeling
|-- Machine Downtime.csv     # Sample dataset
|-- README.md                # Project documentation
```

---

## Notes for Evaluator
1. Open `PredictiveAnalysis.ipynb` in Google Colab or a Jupyter notebook environment.
2. Follow the cell instructions to deploy and test the API.
3. Modify API configuration as needed (e.g., port number or public URL).

I hope this project showcases my ability to integrate machine learning and API development effectively. Thank you for evaluating my work!


