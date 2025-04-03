<h1 align="center" id="title">Dockerized Full Stack Web Application Deployment</h1>

# Frontend - ReactJS with ChakraUI

This directory contains the frontend of the application built with ReactJS and ChakraUI.

<p id="description"> ensure you have the following installed on your local machine:

- Node.js (v14.x or higher)
- npm (v6.x or higher)
    
## Prerequisites

- Node.js (version 14.x or higher)
- npm (version 6.x or higher)

## Setup Instructions

1. **Navigate to the frontend directory**:
    ```sh
    cd frontend
    ```

2. **Install dependencies**:
    ```sh
    npm install
    ```

This command will read the package.json file and install the dependencies listed.

3. **Run the development server**:
    ```sh
    npm run dev
    ```

4. **Configure API URL**:
   Ensure the API URL is correctly set in the `.env` file. The .env file should be located in the root of the frontend directory.

5. **Create a Dockerfile in the frontend directory**
   ```sh
   FROM node:14-alpine
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

6. **Build and Run the Frontend Container**

```sh
docker build -t frontend .
docker run -p 3000:3000 frontend
```


