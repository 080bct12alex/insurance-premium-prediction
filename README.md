# 🚀 Building a Machine Learning-Powered API with FastAPI, Docker & AWS EC2

This project showcases the end-to-end process of:

- 🧠 **Building a machine learning model** (Random Forest) for insurance premium prediction  
- 🧩 **Integrating the model into a FastAPI backend** to expose prediction APIs  
- 🐳 **Containerizing the application using Docker** for portability and consistency  ( easy deployment and consistency across environments.)
- ☁️ **Deploying the service on AWS EC2** to make it globally accessible

It is part of my learning journey in deploying production-ready ML systems using modern backend frameworks and cloud infrastructure.



A FastAPI REST API for predicting insurance premiums based on user data such as BMI, age group, lifestyle risk, city tier, income, and occupation.

---


## 🚀 Features

- A FastAPI REST API for predicting insurance premiums based on user data such as BMI, age group, lifestyle risk, city tier, income, and occupation.
- Predict insurance premiums from structured user inputs
- Uses a **Random Forest** machine learning model for robust predictions


---


---
## ⚙️ Installation & Setup

Follow these steps to set up and run the FastAPI Insurance Premium Prediction API.
---


### ▶️ Option 1: Run Locally (Python)

# 📦 1. **Clone the repository**

git clone https://github.com/yourusername/insurance-premium-prediction.git
cd insurance-premium-prediction/api


 # 🐍 2. Set up virtual environment & install dependencies

python -m venv venv
source venv/bin/activate      # On macOS/Linux
venv\Scripts\activate         # On Windows

pip install -r requirements.txt

🚀 3. Start the FastAPI server

uvicorn main:app --reload 

🌐 4. Access the API locally
Swagger Docs: http://127.0.0.1:8000/docs
Health Check: http://127.0.0.1:8000/health
API Hompage: http://127.0.0.1:8000




## 🐳 Run with Docker

You can containerize the FastAPI application using Docker for easy deployment and consistency across environments.

---


### 📄 1. Create a `Dockerfile` in the `api/` directory if not exist


# Dockerfile
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


🛠️ 2. Build the Docker image
From the api/ directory:

docker build -t insurance-api .


🚀 3. Run the container


docker run -d -p 8000:8000 insurance-api

🌐 4. Access the API in your browser
Swagger UI: http://localhost:8000/docs

Health Check: http://localhost:8000/health


## ☁️ Deploy Docker Container to AWS EC2

You can deploy the Dockerized FastAPI app to a public cloud environment like AWS EC2 by following these steps:

---

### 📦 1. Launch an EC2 Instance

- Use Ubuntu (preferred) or Amazon Linux.
- Make sure to allow **inbound rules** on port `8000` and `22` (SSH) in the security group.

---

### 🔗 2. Connect to the EC2 Instance

ssh -i path/to/your-key.pem ubuntu@<your-ec2-public-ip>

⚙️ 3. Set up Docker on EC2
Run the following commands one-by-one:

sudo apt-get update
sudo apt-get install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
exit

🔄 After running exit, reconnect to apply the Docker group changes.

🔁 4. Reconnect to the EC2 Instance

ssh -i path/to/your-key.pem ubuntu@<your-ec2-public-ip>

🐳 5. Pull and Run the Docker Container

docker pull tweakster24/insurance-premium-api:latest
docker run -d -p 8000:8000 <your-username>/insurance-premium-api

🔐 6. Update Security Group
Go to the AWS EC2 Dashboard → Security Groups:
Edit Inbound Rules
Add a rule to allow HTTP (port 8000) from Anywhere (0.0.0.0/0)

🌐 7. Access the API
Open your browser and visit:
http://<your-ec2-public-ip>:8000/docs

✅ Your Dockerized FastAPI app is now live on AWS EC2!



⚙️ 8. Update the Frontend
Update your frontend API base URL (Point your frontend base URL  to:) to
 
http://<your-ec2-public-ip>:8000

This will point your frontend to the deployed backend.




✅ You now have a fully deployed ML-powered API on the cloud!




---

## 🎨 Frontend (Streamlit)

This project also includes a simple **Streamlit-based frontend UI** for interacting with the FastAPI insurance premium prediction backend.

---

### ▶️ Run Streamlit Frontend Locally

1. From the project root, activate your virtual environment (if not already):

cd frontend
streamlit run frontend.py

The app will run at:
`http://localhost:8501`

Make sure your FastAPI backend is also running  :
> 🔧 In `frontend/frontend.py`, set `API_URL` based on where your backend is running:
> - Local (Python or Docker): `http://localhost:8000/predict`
> - AWS EC2: `http://<your-ec2-public-ip>:8000/predict`













