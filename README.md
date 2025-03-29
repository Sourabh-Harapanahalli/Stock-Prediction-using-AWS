# Stock Prediction and Visualization Platform

## Overview
This project focuses on developing an **end-to-end automated stock analysis and prediction system** leveraging **advanced machine learning techniques** and seamless integration with **AWS services**. The core of the system is a **Long Short-Term Memory (LSTM) model** deployed to predict stock prices based on historical data. A **user-friendly web application**, hosted on **AWS Amplify**, provides secure authentication and intuitive navigation for users to register, log in, and access various features, such as **stock predictions, real-time stock values, and sentiment analysis of current news**.

## Features
- **Secure Authentication**: AWS Cognito ensures user authentication with secure login and registration.
- **Stock Price Forecasting**: LSTM-based predictive model hosted on AWS SageMaker for accurate future price predictions.
- **Real-time Stock Data Retrieval**: Fetches the latest stock values dynamically using Alpha Vantage API.
- **News Aggregation**: Automatically collects and displays the latest stock-related news from News API.
- **Automated Data Updates**: AWS Lambda and CloudWatch automate stock data retrieval and news updates, ensuring up-to-date information.
- **Scalable Cloud Infrastructure**: AWS services enable efficient data processing, scalability, and automation.

## System Architecture
The architecture integrates multiple AWS services to provide a **scalable, serverless, and automated** stock prediction system:

1. **Frontend**: A **React-based** web application hosted on AWS Amplify, providing an interactive user experience.
2. **Authentication**: AWS Cognito secures user access, enabling login and authentication mechanisms.
3. **Backend Services**:
   - **API Gateway**: Manages communication between the frontend and backend services.
   - **Lambda Functions**: Handle stock data retrieval, interaction with the prediction model, and news aggregation.
   - **DynamoDB**: Stores stock-related news data for quick retrieval.
   - **S3**: Serves as the storage for historical stock data used for training and prediction.
   - **SageMaker**: Hosts and deploys the LSTM model for stock price forecasting.
4. **Automation**: AWS CloudWatch schedules tasks for fetching stock data and news updates periodically.

## Technologies Used
- **Cloud Platform**: AWS (Amplify, Lambda, API Gateway, SageMaker, S3, DynamoDB, CloudWatch)
- **Machine Learning**: TensorFlow, LSTM-based time series forecasting
- **Frontend**: React, AWS Amplify
- **Backend**: AWS Lambda, API Gateway, DynamoDB
- **APIs**: Alpha Vantage API (stock data), News API (financial news)

## Installation & Setup
### Prerequisites
- AWS account with required permissions
- Node.js and npm installed
- AWS Amplify CLI installed
- Alpha Vantage API key
- News API key
- Python 3.x installed
- AWS CLI configured

### Steps to Set Up
1. **Clone the repository**:
   ```sh
   git clone https://github.com/Sourabh-Harapanahalli/Stock-Prediction-using-AWS.git
   cd Stock-Prediction-using-AWS
   ```
2. **Install dependencies**:
   ```sh
   npm install
   ```
3. **Set up AWS Amplify**:
   ```sh
   amplify init
   amplify push
   ```
4. **Deploy AWS Lambda functions**:
   - Navigate to `lambda_functions/` and update API keys in `fetch-stock-data.py` & `fetch-news.py`.
   - Deploy Lambda functions using AWS CLI:
     ```sh
     aws lambda create-function --function-name fetchStockData --runtime python3.x --role <IAM_ROLE> --handler fetch-stock-data.lambda_handler --zip-file fileb://fetch-stock-data.zip
     aws lambda create-function --function-name fetchNews --runtime python3.x --role <IAM_ROLE> --handler fetch-news.lambda_handler --zip-file fileb://fetch-news.zip
     ```
5. **Train & Deploy LSTM Model**:
   - Train the model using Jupyter Notebook (`model_training/Sagemaker_Model_Deployment.ipynb`).
   - Deploy it to AWS SageMaker:
     ```sh
     aws sagemaker create-endpoint --endpoint-name stockPredictionEndpoint --endpoint-config-name stockModelConfig
     ```
6. **Set up AWS S3 & DynamoDB**:
   - Create an S3 bucket for storing stock data:
     ```sh
     aws s3 mb s3://stock-prediction-data
     ```
   - Create a DynamoDB table for storing stock news data:
     ```sh
     aws dynamodb create-table --table-name StockNews --attribute-definitions AttributeName=StockSymbol,AttributeType=S --key-schema AttributeName=StockSymbol,KeyType=HASH --billing-mode PAY_PER_REQUEST
     ```
7. **Run the Web Application**:
   ```sh
   npm start
   ```

## Usage
1. **Register/Login**: Secure authentication with AWS Cognito for access control.
2. **Select a Stock**: Users select a stock ticker from the dropdown menu for analysis.
3. **View Predictions**: Click 'Predict' to retrieve stock price forecasts based on historical trends.
4. **Fetch Real-Time Data**: Click 'Current Value' to view the latest stock price.
5. **Retrieve Stock-Related News**: Click 'Top News' to fetch and display relevant financial news articles.

## Demo
The demo showcases the platform’s core capabilities, including:
- Secure user authentication via AWS Cognito.
- Selection of stock tickers and visualization of predictive analysis.
- Real-time retrieval of stock prices.
- Aggregation of latest stock-related news.

## Challenges & Limitations
- **Batch Processing Mode**: The current implementation processes stock data in batches rather than in real time.
- **Cost Considerations**: Running a SageMaker endpoint continuously incurs operational costs.
- **Data Latency**: Real-time analysis requires AWS Kinesis or an alternative streaming solution to process live data.

## Future Enhancements
- **Real-time Analysis with AWS Kinesis**: Implement AWS Kinesis for continuous stock data streaming.
- **Sentiment Analysis Integration**: Utilize Natural Language Processing (NLP) to analyze financial news and social media trends.
- **Hybrid Model Enhancements**: Incorporate Transformer-based architectures to enhance forecasting accuracy.
- **Expanded Data Sources**: Integrate more financial data providers to improve prediction reliability.

## License
This project is licensed under the MIT License.

