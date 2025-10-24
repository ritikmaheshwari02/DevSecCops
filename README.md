# Simple Node.js "Hello World" App

This is a basic Node.js application that serves a "Hello from Node App!" message on port 3000. It includes Dockerfiles for containerization.

## Prerequisites

* [Node.js](https://nodejs.org/) (if running locally without Docker)
* [Docker](https://www.docker.com/)

## Running Locally (Without Docker)

1.  **Install dependencies:**
    ```bash
    npm install
    ```
2.  **Start the server:**
    ```bash
    npm start
    ```
3.  Access the application at `http://localhost:3000`.

## Building and Running with Docker

This project provides two Dockerfiles:

1.  `dockerfile.singlestage`: A straightforward Dockerfile including build tools.
2.  `dockerfile.multistage`: A multi-stage Dockerfile that results in a smaller, potentially more secure production image by excluding build dependencies.

### Single-Stage Build

1.  **Build the image:**
    ```bash
    docker build -t ms-demo:single -f dockerfile.singlestage .
    ```
2.  **Run the container:**
    ```bash
    docker run -p 3000:3000 --name single-stage-app -d ms-demo:single
    ```
3.  Access the application at `http://localhost:3000`.

### Multi-Stage Build

1.  **Build the image:**
    ```bash
    docker build -t ms-demo:multi -f dockerfile.multistage .
    ```
2.  **Run the container:**
    ```bash
    docker run -p 3000:3000 --name multi-stage-app -d ms-demo:multi
    ```
3.  Access the application at `http://localhost:3000`.

## Security Considerations

Security scans (`single_scan.txt` and `multi_scan.txt`) were performed on images built from both Dockerfiles.

* [cite_start]The **single-stage** build (`ms-demo:single`) resulted in a significantly larger number of vulnerabilities (2330 OS vulnerabilities reported)[cite: 1, 21]. This is often due to the inclusion of build-time dependencies and development tools in the final image.
* [cite_start]The **multi-stage** build (`ms-demo:multi`) significantly reduced the number of OS vulnerabilities (88 reported)[cite: 1999, 2000]. This demonstrates the security benefit of using multi-stage builds to create leaner production images containing only runtime essentials.

[cite_start]Both scans also identified 2 Node.js package vulnerabilities (brace-expansion and cross-spawn)[cite: 6, 7, 1996, 2027, 2034]. These should be addressed by updating the dependencies if possible.

**Note:** Always scan your container images for vulnerabilities before deploying to production.
