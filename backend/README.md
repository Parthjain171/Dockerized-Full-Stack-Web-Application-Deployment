<h1 align="center" id="title">Dockerized Full Stack Web Application Deployment</h1>

## Frontend - ReactJS with ChakraUI

This directory contains the frontend of the application built with **ReactJS** and **ChakraUI**.

<p id="description">Ensure you have the following installed on your local machine:</p>

- **Node.js** (v14.x or higher)  
- **npm** (v6.x or higher)  

---

## Prerequisites

- **Node.js** (version 14.x or higher)  
- **npm** (version 6.x or higher)  

---

## Setup Instructions

### 1️⃣ Navigate to the frontend directory  
```sh
cd frontend
```

### 2️⃣ Install dependencies
```sh
npm install
```

This command will read the package.json file and install the dependencies listed.

### 3️⃣ Run the development server:
```sh
npm run dev
```

### 4️⃣ Configure API URL:
Ensure the API URL is correctly set in the `.env` file. The .env file should be located in the root of the frontend directory.

### 5️⃣ Create a Dockerfile in the frontend directory
```dockerfile
FROM node:14-alpine
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

### 6️⃣ Build and Run the Frontend Container
```sh
docker build -t frontend .
docker run -p 3000:3000 frontend
```

---

## Backend - FastAPI with PostgreSQL

This directory contains the backend of the application built with FastAPI and a PostgreSQL database.

### Cloud Deployment

#### Deploy AWS EC2 instance

Launch an EC2 Instance:
- Choose an Amazon Machine Image (AMI) such as Ubuntu 20.04.
- Select an instance type (e.g., t3 medium as the application is robust).
- Configure security groups to allow HTTP (port 80) and HTTPS (port 443) traffic and custom TCP and set it anywhere.

![ec2 instance](https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/3f5df5c0-a7c6-4b9a-9abb-c8206581e974)

#### Install Docker and Docker Compose
```sh
sudo apt update
sudo apt install docker.io docker-compose -y
sudo usermod -aG docker ${USER}
newgrp docker
```

#### Deploy Your Application
```sh
docker-compose up -d
```

---

## Prerequisites
- Python 3.8 or higher
- Poetry (for dependency management)
- PostgreSQL (ensure the database server is running)

### Installing Poetry
```sh
curl -sSL https://install.python-poetry.org | python3 -
```
Add Poetry to your PATH (if not automatically added):

---

## Setup Instructions

### 1️⃣ Navigate to the backend directory:
```sh
cd backend
```

### 2️⃣ Install dependencies using Poetry:
```sh
poetry install
```

### 3️⃣ Create a Dockerfile in the backend directory
```dockerfile
FROM python:3.8-slim
WORKDIR /app
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### 4️⃣ Build and Run the Backend Container
```sh
docker build -t backend .
docker run -p 8000:8000 backend
```

### 5️⃣ Create a Docker Compose file Using Nginx Proxy Manager

![docker c1](https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/9f766f1c-e7d5-4f3a-81aa-1efd05c083ad)

![docker c2](https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/1da81442-6865-47e5-88a6-13f8480abcac)

![docker c3](https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/5ff72e12-5aa5-4a58-a3e5-58d64278816b)

![docker c4](https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/cac8b19d-6866-4b05-90e5-a3d55dd61e77)

![docker c5](https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/9291a744-6f6b-4232-8f18-777da24b6b75)

### 6️⃣ Deploy the Services:
```sh
docker-compose up -d
```

### 7️⃣ Database Configuration
Ensure your FastAPI application is configured to connect to the PostgreSQL database. Update your FastAPI application to use the PostgreSQL URL:
```sh
DATABASE_URL = "postgresql://user:password@db:5432/database"
```

### 8️⃣ Adminer Setup
Configure Adminer to run on port 8080 and ensure it is accessible via the subdomain db.yourdomain.com

### 9️⃣ Proxy Manager Setup
Configure Nginx Proxy Manager to run on port 8090 and ensure it is accessible via the subdomain proxy.yourdomain.com.

### 🔟 Set up the database with the necessary tables:
```sh
poetry run bash ./prestart.sh
```

### 1️⃣1️⃣ Run the backend server:
```sh
poetry run uvicorn app.main:app --reload
```

### 1️⃣2️⃣ Update configuration:
Ensure you update the necessary configurations in the `.env` file, particularly the database configuration.

### 1️⃣3️⃣ Set Up Domain and HTTPS
Obtain a Free Subdomain from Afraid DNS by registering and configuring your subdomain. By following these steps, you will successfully deploy your full stack web application using Docker and a reverse proxy, ensuring it is accessible on the web with a properly configured domain.

![postgresql](https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/f1e1e906-cef0-45b9-bc96-95f754ae646b)

![proxy manager](https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/d676d8f0-a6f7-4a9d-9f88-66ca538bbedb)

![subdomain](https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/844d3961-fde0-412c-b01a-40143c119b17)

![postgressql2](https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/de640cba-cba1-4856-a996-7378c3ba27fc)

![docs1](https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/91ec2ce4-54e6-4655-80b1-d3b6e9ae8e91)

![docs 2](https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/04f7a502-e08e-49f9-9ad1-0e9591ef1e9a)

