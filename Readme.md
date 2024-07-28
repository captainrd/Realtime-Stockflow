# Stock Market Kafka Real-Time Data Engineering Project
=====================================================

## Introduction
---------------

This project outlines a robust end-to-end data engineering pipeline for processing and analyzing real-time stock market data. It leverages a combination of powerful technologies:

*   Python: For developing data processing and manipulation scripts.
*   Amazon Web Services (AWS):
    *   S3 (Simple Storage Service): For efficiently storing large volumes of stock market data.
    *   Athena: For interactive querying of the stored data using standard SQL.
    *   Glue Crawler: To automatically discover and catalog the data schema in S3.
    *   Glue Catalog: To provide a centralized metadata store for managing data assets.
    *   EC2 (Elastic Compute Cloud): As the underlying infrastructure to run the data pipeline.
*   Apache Kafka: A distributed streaming platform for ingesting and processing real-time stock market data feeds.

This project offers a valuable foundation for building real-time stock market data analysis applications.

## Architecture
------------

### Key Components

*   Real-time Stock Market Data Feed: Source of the data stream (e.g., financial APIs, web scraping).
*   Apache Kafka Producer: Publishes data to the Kafka topic.
*   Kafka Topic: A dedicated channel within Kafka for data streaming.
*   Kafka Consumer: Receives data from the topic and performs necessary processing.
*   S3 Bucket: Stores historical and curated stock market data in a scalable and cost-effective manner.
*   Glue Crawler and Catalog: Automate schema discovery and maintain data lineage for improved data management.
*   Athena: Allows querying the data directly in S3 using SQL.
*   Analytics and Visualization Tools: (Optional) Explore and derive insights from the processed data (e.g., Python libraries like Matplotlib, Seaborn, or interactive dashboards).

### Technology Stack

*   Programming Language: Python
*   AWS Services:
    *   S3
    *   Athena
    *   Glue Crawler
    *   Glue Catalog
    *   EC2
*   Other Tools: Apache Kafka

### Dataset Considerations

The project is flexible and can accommodate various stock market data sources. For illustrative purposes, you can utilize the dataset provided in the reference video: <https://github.com/darshilparmar/stock-market-kafka-data-engineering-project/blob/main/indexProcessed.csv>

## Setup and Configuration Instructions
--------------------------------------

Detailed setup instructions will vary depending on your environment and infrastructure choices. However, here's a general outline:

### 1. EC2 Instance Setup

*   Create an EC2 Instance: Launch an EC2 instance in your preferred AWS region. Ensure it has the necessary resources (CPU, memory, storage) to handle the data pipeline workload.
*   Configure Security Groups: Open necessary ports for Kafka communication (e.g., port 9092).
*   Connect to EC2 Instance: Use SSH to connect to your EC2 instance for further configuration.

### 2. Install Java (if not already installed)

```bash
java -version
sudo yum install java  # Or equivalent command for your Linux distribution


### 3. Download and Extract Apache Kafka

wget https://downloads.apache.org/kafka/3.7.1/kafka_2.13-3.7.1.tgz
tar -xvf kafka_2.13-3.7.1.tgz
cd kafka_2.13-3.7.1

4. Start ZooKeeper and Kafka Server
bin/zookeeper-server-start.sh config/zookeeper.properties
# Open a new terminal
export KAFKA_HEAP_OPTS="-Xmx256M -Xms128M"
cd kafka_2.13-3.7.1
bin/kafka-server-start.sh config/server.properties

Note:

Ensure server.properties is configured to use your EC2 instance's public IP address (edit the ADVERTISED_LISTENERS property using sudo nano config/server.properties).
If you encounter issues, verify necessary ports are open in your security group settings.

5. Create Kafka Topics
cd kafka_2.13-3.7.1
bin/kafka-topics.sh --create --topic stock_market_data --bootstrap-server <YOUR_PUBLIC_IP>:9092 --replication-factor 1 --partitions 1

Replace <YOUR_PUBLIC_IP> with the actual public IP address of your EC2 instance. This command creates a Kafka topic named stock_market_data with one partition and replication factor of 1. Adjust the number of partitions and replication factor based on your specific requirements.

6. Configure Kafka Producer
