# Credit Card Default Prediction

## Problem Statement
This project aims to develop a classification model to predict whether a customer will default on their credit card payment in the next month. Accurate predictions will enable the bank to estimate cash inflows, manage financial risk, and optimize budget planning. By analyzing historical payment data, the model will identify high-risk customers, helping the bank to minimize losses and strategize effectively.

## Sections
1. [Dataset Description](dataset/README.md)
2. [Training Workflow](training/README.md)
3. [Prediction Workflow](prediction/README.md)

## Application Flow
<img src="assets\appFlow.png" alt="Thyroid Classification Overview" width="500" height="500">

## Run Locally

1. Clone the project
```bash
  git https://github.com/N1RM4L13/CreditCardDefault.git
```

2. Install dependencies
```bash
  pip install -r requirements.txt
```

3. Start the Service

```bash
  python main.py
```

4. The API will start running on http://127.0.0.1:5000 by default (or any specified port in your configuration).

5. You can test the API using tools like Postman or cURL.

To test the API, use the following cURL command with JSON input:
```bash
curl -X POST http://127.0.0.1:5000/predict \
-H "Content-Type: application/json" \
-d '{"filepath":"Prediction_Batch_Files"}'
```
Alternatively, if you prefer to use localhost instead of the IP address, you can replace http://127.0.0.1:5000 with http://localhost:5000 in the cURL command.

## Use Case
The classification model will help the bank in the following ways:
1. **Cash Flow Optimization**: Predict repayment inflows to allocate resources efficiently.  
2. **Risk Assessment**: Identify high-risk customers to mitigate financial losses.  
3. **Strategic Budgeting**: Align financial strategies with repayment predictions for effective planning.
