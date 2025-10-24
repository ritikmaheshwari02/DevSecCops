Hello\! As requested, I have edited the text to remove all emojis.

Here is the cleaned-up version of the text:

-----

# node-app

# Assignment 2 – Multi-Stage Dockerfile (Node.js)

## Objective

Build a minimal runtime Docker image for a Node.js application using multi-stage builds.

-----

## Project Structure

## node-app/ ├── app.js ├── package.json ├── Dockerfile └── README.md

## Step 1: Simple Node.js App

The app starts a basic HTTP server on port 3000 and returns a simple message.

app.js

```javascript
const http = require('http');
const port = 3000;
const server = http.createServer((req, res) => {
  res.end('Hello from Docker Multi-Stage Build!');
});
server.listen(port, () => console.log(`Running on port ${port}`));
```

-----

## Step 2: Multi-Stage Dockerfile

This Dockerfile uses two stages:

1.  Builder Stage – installs dependencies.
2.  Runtime Stage – copies only the necessary files to make the image lightweight.

Dockerfile

```dockerfile
# Stage 1: Build stage
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

# Stage 2: Runtime stage
FROM node:18-slim
WORKDIR /app
COPY --from=builder /app .
EXPOSE 3000
CMD ["node", "app.js"]
```

-----

## Step 3: Build and Run Docker Image

### Build Image

`docker build -t multi-stage-node .`

### Run Container

`docker run -d -p 3000:3000 multi-stage-node`

### Test Application

`curl http://localhost:3000`

## Expected Output: `Hello from Docker Multi-Stage Build!`

## Step 4: Compare Image Sizes

| Build Type | Command | Image Size |
|---|---|---|
| Single-Stage Build | `docker build -t single .` | Larger (\~1GB) |
| Multi-Stage Build | `docker build -t multi .` | Smaller (\~200MB) |

Screenshot Required:
Take a screenshot of `docker images` showing both image sizes.

-----

## Expected Screenshots

  - `docker images` size comparison
  - Running container output (`curl http://localhost:3000`)
  - Dockerfile code snippet

-----

## Notes

  - Multi-stage builds reduce final image size by removing unnecessary build files.
  - `node:18-slim` is used for a smaller runtime environment.
  - Exposed port 3000 is used to access the application in browser:
    `http://localhost:3000`

-----

## Conclusion

Using multi-stage builds significantly reduces Docker image size and improves deployment efficiency.
This project demonstrates how to build, run, and optimize a Node.js Docker container.

-----

I have provided the full text with the requested emoji removal. Do you need any further assistance or changes to this text?
