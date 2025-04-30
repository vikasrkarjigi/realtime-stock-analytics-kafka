# Real-Time Stock Market Data Analysis Using Apache Kafka and AWS

## Project Badges

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=ffffff)
![Apache Kafka](https://img.shields.io/badge/Apache_Kafka-2.8.0-ff69b4?logo=apachekafka&logoColor=ffffff)
![AWS DynamoDB](https://img.shields.io/badge/AWS_DynamoDB-4053D6?logo=amazonaws&logoColor=ffffff)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas)
![Numpy](https://img.shields.io/badge/Numpy-013243?logo=numpy)
![Matplotlib](https://img.shields.io/badge/Matplotlib-0077BB?logo=matplotlib)
![Seaborn](https://img.shields.io/badge/Seaborn-0C4B8E?logo=python&logoColor=ffffff)
![Real-Time Processing](https://img.shields.io/badge/Real--Time%20Processing-4CAF50?logo=real-time&logoColor=ffffff)


## 🧠 Description

This project demonstrates a **real-time data pipeline** for analyzing stock market data using **Apache Kafka**, **AWS EC2**, and **DynamoDB**. Stock prices from leading companies (NVIDIA, Tesla, Meta, Amazon, Apple, Netflix, Google) are streamed in real-time using Kafka and stored in DynamoDB, where they are later queried and visualized to reveal investment insights and trends.

---

## 📁 Project Structure

```text
├── Kafka_Producer.ipynb                 # Streams stock data from CSV to Kafka topic  
├── Kafka_Consumer.ipynb                 # Listens to Kafka and writes data to DynamoDB  
├── stock_data_april2023_to_apr2025.csv  # Stock price dataset (April 2023 to April 2025)  
├── stock_data_ingestion_and_cleaning.ipynb  # Data ingestion, cleaning, and EDA  
├── kafka_stock_analysis_visuals.ipynb       # Visualizations: line plots, heatmaps, box plots  
├── BDT Project Workflow.pdf             # Step-by-step setup guide (Kafka, EC2, DynamoDB)  
└── README.md                            # Project documentation
```

---

## 🔧 Tools & Technologies

- **Apache Kafka** – Stream processing with Producer & Consumer
- **AWS EC2** – Kafka broker hosted on a cloud VM
- **AWS DynamoDB** – NoSQL database to store streaming data
- **Python Libraries**:
  - `pandas`, `numpy` – Data processing
  - `matplotlib`, `seaborn` – Visualization
  - `kafka-python`, `boto3` – Kafka & AWS integration

---

## 📉 Dataset

- **Source**: Yahoo Finance (`yfinance` Python package)
- **Period**: April 1, 2023 – April 15, 2025
- **Companies**: NVIDIA, Tesla, Meta, Amazon, Apple, Netflix, Google
- **Features**:
  - `Date`, `Open`, `High`, `Low`, `Close`, `Volume`, `Company Name`

---

## 🚀 Pipeline Workflow

1. **Data Collection & Cleaning**
   - Dataset fetched via `yfinance` and saved as CSV.
   - Missing values imputed or removed.
   - Dataset cleaned and transformed for streaming.

2. **Kafka Producer**
   - Reads the dataset row-by-row.
   - Sends each record as JSON to Kafka topic `demo`.

3. **Kafka Broker on EC2**
   - Hosted using Amazon Linux 2.
   - Kafka broker listens on public IP (`PLAINTEXT://<EC2_IP>:9092`).

4. **Kafka Consumer**
   - Listens to topic `demo`, receives JSON data.
   - Inserts records into DynamoDB table `StockMkt`.

5. **DynamoDB Table**
   - Partition Key: `Company Name`
   - Sort Key: `Date`
   - Queried for real-time insights via AWS Console or Python.

6. **Data Analysis & Visualization**
   - Line plots: Stock trends for 10, 30, 50 days
   - Box plots: Distribution of prices
   - Heatmaps: Correlation among `Open`, `Close`, `High`, `Low`, `Volume`

---

## 📊 Visual Insights

- **Netflix** showed the most significant upward trend.
- **Meta** and **NVIDIA** had strong positive correlation between opening and closing prices.
- **Tesla** and **Google** exhibited greater volatility.
- **Heatmap** analysis confirmed strong inter-feature relationships useful for investment decisions.

---

## ✅ How to Run the Project

> Ensure you have AWS credentials, a running EC2 instance, and ports/security groups configured properly.

1. **Launch EC2 & Kafka**
   - Follow `BDT Project Workflow.pdf` for setup.
   - Start Zookeeper & Kafka broker on EC2.

2. **Run the Kafka Producer**
   - In `Kafka_Producer.ipynb`, update the EC2 IP.
   - Send data from CSV to Kafka topic.

3. **Run the Kafka Consumer**
   - In `Kafka_Consumer.ipynb`, receive data from Kafka and insert into DynamoDB.

4. **Visualize the Data**
   - Use `kafka_stock_analysis_visuals.ipynb` to generate insights and graphs.

---

## 🔐 AWS IAM Setup

- Create IAM user with **AmazonDynamoDBFullAccess**
- Use `boto3` to authenticate using Access Key and Secret

---

## 📎 References

- [Apache Kafka Documentation](https://kafka.apache.org/documentation/)
- [Amazon DynamoDB](https://docs.aws.amazon.com/dynamodb/)
- [Yahoo Finance API (`yfinance`)](https://pypi.org/project/yfinance/)
- [boto3 AWS SDK for Python](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html)

