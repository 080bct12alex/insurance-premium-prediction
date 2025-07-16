
# 🚀 Building End-to-End  Machine Learning-Powered Insurance Premium System: FastAPI API + Docker + AWS EC2 + Streamlit UI

This project showcases the end-to-end process of:

- 🧠 **Building a machine learning model** (Random Forest) for insurance premium prediction  
- 🧩 **Integrating the model into a FastAPI backend** to expose prediction APIs  
- 🐳 **Containerizing the application using Docker** for portability  ( easy deployment and consistency across environments.)
- ☁️ **Deploying the service on AWS EC2** to make it globally accessible  

> It is part of my learning journey in deploying production-ready ML systems using modern backend frameworks and cloud infrastructure.

---

## 🔍 Overview

A FastAPI REST API for predicting insurance premiums based on user data such as:

- BMI  
- Age group  
- Lifestyle risk  
- City tier  
- Income  
- Occupation  

---

## 🚀 Features

- ✅ REST API built with **FastAPI**  
- 🧠 Predict insurance premiums using a **Random Forest** model  from structured user inputs
- 🔗 API documented with **Swagger UI**  
- 🐳 Docker support for easy deployment  
- ☁️ Cloud-hosted on **AWS EC2**  
- 🎨 Includes a **Streamlit frontend** for live interaction  

---

## ⚙️ Installation & Setup

### ▶️ Option 1: Run Locally (Python)

#### 📦 Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/insurance-premium-prediction.git
cd insurance-premium-prediction/api
```

#### 🐍 Step 2: Set Up Virtual Environment & Install Dependencies

```bash
python -m venv venv
source venv/bin/activate      # macOS/Linux
venv\Scripts\activate         # Windows

pip install -r requirements.txt
```

#### 🚀 Step 3: Start the FastAPI Server

```bash
uvicorn main:app --reload
```

#### 🌐 Step 4: Access the API

- Swagger Docs: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)  
- Health Check: [http://127.0.0.1:8000/health](http://127.0.0.1:8000/health)
- API Hompage: [http://127.0.0.1:8000](http://127.0.0.1:8000)

---

## 🐳 Run with Docker


### 📄 Step 1: Create a `Dockerfile` (if not present in `/api/`)

```dockerfile
# Use Python 3.11 base image
FROM python:3.11-slim

# Set working directory
WORKDIR /app

# Copy requirements and install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy rest of application code
COPY . .

# Expose the application port
EXPOSE 8000

# Command to start FastAPI application
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]

```

### 🛠️ Step 2: Build the Docker Image

```bash
docker build -t insurance-api .
```

### 🚀 Step 3: Run the Docker Container

```bash
docker run -d -p 8000:8000 insurance-api
```

### 🌐 Step 4: Access the API

- Swagger Docs: [http://localhost:8000/docs](http://localhost:8000/docs)  
- Health Check: [http://localhost:8000/health](http://localhost:8000/health)

---

## ☁️  Deploy Docker Container to AWS EC2

You can deploy the Dockerized FastAPI app to a public cloud environment like AWS EC2 by following these steps:


### 📦 Step 1: Launch an EC2 Instance

- Use **Ubuntu** (preferred) or **Amazon Linux**  
- Allow inbound rules in the security group for:
  - Port `22` (SSH)  
  - Port `8000` (API access)


   
### 🔗 Step 2: Connect to EC2 Instance

```bash
ssh -i path/to/your-key.pem ubuntu@<your-ec2-public-ip>
```

### ⚙️ Step 3: Setup and Install Docker on EC2 
 Run the following commands one-by-one:

```bash
sudo apt-get update
sudo apt-get install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
exit
```
🔄 After running exit, reconnect to apply the Docker group changes.
> 🔁 Reconnect to the EC2 Instance after `exit`:

```bash
ssh -i path/to/your-key.pem ubuntu@<your-ec2-public-ip>
```

### 🐳 Step 4: Pull and Run the Docker Image

```bash
docker pull <your-username>/insurance-premium-api:latest
docker run -d -p 8000:8000 <your-username>/insurance-premium-api
```

### 🔐 Step 5: Configure Security Group

- In AWS EC2 Dashboard → **Security Groups**  
- Edit Inbound Rules to allow HTTP on port `8000` from  Anywhere `0.0.0.0/0`

### 🌐 Step 6: Access the API

Open your browser:

```
http://<your-ec2-public-ip>:8000/docs
```
✅ Your Dockerized FastAPI app is now live on AWS EC2!
---

✅ Your Dockerized FastAPI app is now live on AWS EC2!

✅ You now have a fully deployed ML-powered API on the cloud!

## 🖼️ Frontend (Streamlit)
This project also includes a simple Streamlit-based frontend UI for interacting with the FastAPI insurance premium prediction backend.

### ▶️ Run Streamlit Frontend Locally
From the project root:
```bash
cd frontend
```
Activate your virtual environment :

Install streamlit:
```bash
pip install streamlit
```
Run the Streamlit app:
```bash
streamlit run frontend.py
```

- The app will runs at: `http://localhost:8501`

### 🔧 Set Backend API URL in `frontend/frontend.py`:

```python
# For local backend  and docker
API_URL = "http://localhost:8000/predict"

# For deployed backend on AWS EC2
API_URL = "http://<your-ec2-public-ip>:8000/predict"
```

---

## 📫  Note

- 🔄 Restart your Docker container on EC2 to apply code or model updates  
- 📦 Rebuild your Docker image if you change dependencies (`requirements.txt`)  
- 🔧 Make sure port 8000 is open in your EC2 security group  


---
## 🚀 Final Notes for improvements :

- 🤖 **Add CI/CD** using **GitHub Actions** to:
  - Automatically build and push Docker images to Docker Hub
  - Optionally deploy to EC2 using SSH or GitHub self-hosted runners
- 📈 **Add model versioning or monitoring** automatically  using tools like MLflow
- 🌍 **Add support for HTTPS** via a reverse proxy like Nginx with SSL
- - 🧪 **Integrate unit tests** for input validation and prediction  using pytest
- 📊 **Add logging and error tracking** (e.g., via Loguru or Sentry)
- 📉 Add performance monitoring (e.g., Prometheus + Grafana or Sentry tracing)
- 🔐 Add authentication and authorization to secure the API using tools like JWT (via OAuth2), API Keys, or Auth Providers (e.g., Auth0, Firebase)


---




