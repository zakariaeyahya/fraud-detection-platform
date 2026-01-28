# Fraud Detection Platform

[![Java](https://img.shields.io/badge/Java-17-orange.svg)](https://openjdk.org/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-4.0-green.svg)](https://spring.io/projects/spring-boot)
[![Kafka](https://img.shields.io/badge/Apache%20Kafka-3.x-black.svg)](https://kafka.apache.org/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

> Real-time banking fraud detection system using Machine Learning and microservices architecture.

## Overview

This platform detects fraudulent banking transactions in real-time using machine learning models. Built with a microservices architecture, it processes high-volume transaction streams through Apache Kafka and provides instant fraud scoring.

## Architecture

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Transaction   │     │                 │     │   ML Fraud      │
│   Simulator     │────▶│  Apache Kafka   │────▶│   Detection     │
│                 │     │                 │     │   Service       │
└─────────────────┘     └─────────────────┘     └────────┬────────┘
                                                         │
                                                         ▼
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Dashboard     │◀────│   API Gateway   │◀────│   PostgreSQL    │
│   (Frontend)    │     │   (Express.js)  │     │   + Redis       │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

## Microservices

| Service | Description | Tech Stack | Port |
|---------|-------------|------------|------|
| **transaction-simulator** | Generates realistic banking transactions | Spring Boot, Kafka Producer | 8081 |
| **fraud-detection-service** | ML-based fraud scoring engine | Python, Scikit-learn, Kafka Consumer | 8082 |
| **api-gateway** | Central API routing & authentication | Express.js, JWT | 8080 |
| **dashboard** | Real-time monitoring interface | React, Chart.js | 3000 |

## Tech Stack

### Backend
- **Java 17** + **Spring Boot 4** - Microservices framework
- **Apache Kafka** - Event streaming platform
- **PostgreSQL** - Persistent storage
- **Redis** - Caching & session management

### Machine Learning
- **Python 3.10+**
- **Scikit-learn** - ML models
- **Pandas** - Data processing
- **XGBoost** / **Random Forest** - Fraud classification

### Frontend
- **React 18** - Dashboard UI
- **Chart.js** - Real-time visualizations
- **Material-UI** - Component library

### Infrastructure
- **Docker** + **Docker Compose** - Containerization
- **Kubernetes** (optional) - Orchestration

## Quick Start

### Prerequisites

- Java 17+
- Node.js 18+
- Python 3.10+
- Docker & Docker Compose
- Apache Kafka

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/YOUR_USERNAME/fraud-detection-platform.git
cd fraud-detection-platform
```

2. **Start infrastructure services**
```bash
docker-compose up -d kafka zookeeper postgres redis
```

3. **Run the Transaction Simulator**
```bash
cd transaction-simulator
./mvnw spring-boot:run
```

4. **Run the Fraud Detection Service**
```bash
cd fraud-detection-service
pip install -r requirements.txt
python main.py
```

5. **Run the API Gateway**
```bash
cd api-gateway
npm install
npm start
```

6. **Run the Dashboard**
```bash
cd dashboard
npm install
npm run dev
```

## Configuration

### Environment Variables

```env
# Kafka
KAFKA_BOOTSTRAP_SERVERS=localhost:9092
KAFKA_TOPIC_TRANSACTIONS=transactions
KAFKA_TOPIC_FRAUD_ALERTS=fraud-alerts

# Database
POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_DB=fraud_detection
POSTGRES_USER=admin
POSTGRES_PASSWORD=your_password

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379

# ML Model
MODEL_PATH=./models/fraud_model.pkl
FRAUD_THRESHOLD=0.7
```

## API Endpoints

### Transactions
```
POST   /api/transactions          # Submit new transaction
GET    /api/transactions/:id      # Get transaction details
GET    /api/transactions/fraud    # List flagged transactions
```

### Analytics
```
GET    /api/analytics/dashboard   # Dashboard metrics
GET    /api/analytics/trends      # Fraud trends over time
GET    /api/analytics/stats       # Statistical summaries
```

### Alerts
```
GET    /api/alerts                # List all alerts
PUT    /api/alerts/:id/resolve    # Mark alert as resolved
```

## Machine Learning Model

### Features Used
- Transaction amount
- Time of transaction
- Merchant category
- Geographic location
- Transaction frequency
- Account age
- Historical patterns

### Model Performance
| Metric | Score |
|--------|-------|
| Accuracy | 98.5% |
| Precision | 97.2% |
| Recall | 96.8% |
| F1-Score | 97.0% |

## Project Structure

```
fraud-detection-platform/
├── transaction-simulator/     # Java Spring Boot
│   ├── src/
│   ├── pom.xml
│   └── README.md
├── fraud-detection-service/   # Python ML Service
│   ├── models/
│   ├── src/
│   ├── requirements.txt
│   └── README.md
├── api-gateway/               # Express.js
│   ├── src/
│   ├── package.json
│   └── README.md
├── dashboard/                 # React Frontend
│   ├── src/
│   ├── package.json
│   └── README.md
├── docker-compose.yml
├── .env.example
└── README.md
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Authors

- **Your Name** - *Initial work*

## Acknowledgments

- Kaggle Credit Card Fraud Dataset
- Apache Kafka Documentation
- Spring Boot Community
