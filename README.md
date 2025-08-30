# DevOps Coursework 2

This project is a simple Node.js web server that serves as a basic example for a DevOps pipeline. The server responds to HTTP requests on port 8080 with a plain text message.

## Getting Started

To run this application locally, you will need to have Docker installed.

1.  **Build the Docker image:**

    Open your terminal in the project root and run the following command to build the Docker image:

    ```bash
    docker build -t coursework2 .
    ```

2.  **Run the Docker container:**

    After the image is built, you can run the application in a Docker container with this command:

    ```bash
    docker run -p 8080:8080 -d coursework2
    ```

3.  **Access the application:**

    You can now access the application by navigating to `http://localhost:8080` in your web browser or by using a tool like `curl`:

    ```bash
    curl http://localhost:8080
    ```

    You should see a response similar to this:
    `DevOps Coursework 2! | Running on: <container_hostname> | v=3`

## Deployment

This project is configured with a continuous integration and deployment (CI/CD) pipeline using Jenkins. The pipeline is defined in the `Jenkinsfile` and performs the following stages:

1.  **Build**: The pipeline checks out the source code from the `main` branch and builds a Docker image named `jscott1997/coursework2`.
2.  **Test**: A placeholder test stage is run to ensure the application passes basic checks.
3.  **Deploy**:
    *   The pipeline logs into Docker Hub and pushes the newly built Docker image.
    *   It then connects to a production server via SSH and updates the Kubernetes deployment (`coursework2`) to use the new Docker image, effectively deploying the new version of the application.
