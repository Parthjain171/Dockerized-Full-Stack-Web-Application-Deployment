# Backend - FastAPI with PostgreSQL

This directory contains the backend of the application built with FastAPI and a PostgreSQL database.


**Cloud Deployment**
Deploy AWS EC2 instance
Launch an EC2 Instance:

Choose an Amazon Machine Image (AMI) such as Ubuntu 20.04.
Select an instance type (e.g., t3 medium as the application is robust).
Configure security groups to allow HTTP (port 80) and HTTPS (port 443) traffic and custom TCP and set it anywhere.

<img width="959" alt="ec2 instance" src="https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/3f5df5c0-a7c6-4b9a-9abb-c8206581e974">

**Install Docker and Docker Compose**
On the terminal, install docker and docker compose using the below commands

```sh
sudo apt update
sudo apt install docker.io docker-compose -y
sudo usermod -aG docker ${USER}
newgrp docker
```
**Deploy Your Application**

```sh
docker-compose up -d
```


## Prerequisites

- Python 3.8 or higher
- Poetry (for dependency management)
- PostgreSQL (ensure the database server is running)

### Installing Poetry

To install Poetry, follow these steps:

```sh
curl -sSL https://install.python-poetry.org | python3 -
```

Add Poetry to your PATH (if not automatically added):

## Setup Instructions

1. **Navigate to the backend directory**:
    ```sh
    cd backend
    ```

2. **Install dependencies using Poetry**:
    ```sh
    poetry install
    ```

3. **Create a Dockerfile in the backend directory**

   ```sh
    FROM python:3.8-slim
    WORKDIR /app
    COPY requirements.txt ./
    RUN pip install --no-cache-dir -r requirements.txt
    COPY . .
    EXPOSE 8000
    CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
   ```


4. **Build and Run the Backend Container**
   ```sh
   docker build -t backend .
   docker run -p 8000:8000 backend
   ```

5. **Create a Docker Compose file Using Nginx Proxy Manager**

   
<img width="959" alt="docker c1" src="https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/9f766f1c-e7d5-4f3a-81aa-1efd05c083ad">

<img width="959" alt="docker c2" src="https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/1da81442-6865-47e5-88a6-13f8480abcac">

<img width="959" alt="docker c3" src="https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/5ff72e12-5aa5-4a58-a3e5-58d64278816b">

<img width="959" alt="docker c4" src="https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/cac8b19d-6866-4b05-90e5-a3d55dd61e77">

<img width="953" alt="docker c5" src="https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/9291a744-6f6b-4232-8f18-777da24b6b75">


6. **Deploy the Services:**

   ```sh
   docker-compose up -d
   ```

7. **Database Configuration**
   Ensure your FastAPI application is configured to connect to the PostgreSQL database. Update your FastAPI application to use the PostgreSQL URL:
   ```sh
   DATABASE_URL = "postgresql://user:password@db:5432/database"
   ```

8. **Adminer Setup**
   Configure Adminer to run on port 8080 and ensure it is accessible via the subdomain db.yourdomain.com

9. **Proxy Manager Setup**
   Configure Nginx Proxy Manager to run on port 8090 and ensure it is accessible via the subdomain proxy.yourdomain.com.
   
10. **Set up the database with the necessary tables**:
    ```sh
    poetry run bash ./prestart.sh
    ```

11. **Run the backend server**:
    ```sh
    poetry run uvicorn app.main:app --reload
    ```
12. **Update configuration**:
   Ensure you update the necessary configurations in the `.env` file, particularly the database configuration.

13. **Set Up Domain and HTTPS**
    Obtain a Free Subdomain from Afraid DNS by registering and configuring your subdomain.
    By following these steps, you will successfully deploy your full stack web application using Docker and a reverse proxy, ensuring it is accessible on the web with a 
    properly configured domain.
    The pictures confirms the steps above:

    <img width="957" alt="postgresql" src="https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/f1e1e906-cef0-45b9-bc96-95f754ae646b">


    <img width="959" alt="proxy manager" src="https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/d676d8f0-a6f7-4a9d-9f88-66ca538bbedb">


    <img width="959" alt="subdomain" src="https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/844d3961-fde0-412c-b01a-40143c119b17">


     <img width="959" alt="postgressql2" src="https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/de640cba-cba1-4856-a996-7378c3ba27fc">


     <img width="949" alt="docs1" src="https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/91ec2ce4-54e6-4655-80b1-d3b6e9ae8e91">


<img width="944" alt="docs 2" src="https://github.com/Iyewumi-Adesupo/Dockerized-Full-Stack-Web-Application-Deployment/assets/135404420/04f7a502-e08e-49f9-9ad1-0e9591ef1e9a">
