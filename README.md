# DevOps Mini Project

A Python Flask application for practising automated testing, Docker containerization, Git version control, and Continuous Integration (CI) with GitHub Actions.

## 1. Project Objectives

- Build a simple Flask web application.
- Write automated tests using pytest.
- Package the application into a Docker image.
- Run and verify the application inside a Docker container.
- Automate Python tests and Docker image builds using GitHub Actions.

## 2. Technology Stack

- **Application:** Python 3.12, Flask
- **Testing:** pytest
- **Containerization:** Docker Engine
- **Version Control:** Git and GitHub
- **CI:** GitHub Actions
- **Development Environment:** Ubuntu on WSL

## 3. Application Endpoints

| Endpoint | Purpose | Expected result |
|---|---|---|
| `/` | Returns the welcome message and application status | HTTP 200 |
| `/health` | Reports application health | HTTP 200 |

Example health response:

```json
{"status": "healthy"}
```

## 4. Project Structure

```text
devops-mini-project/
├── .github/
│   └── workflows/
│       └── ci.yml
├── .dockerignore
├── .gitignore
├── Dockerfile
├── app.py
├── requirements.txt
└── test_app.py
```

## 5. Docker Configuration

The Docker image uses `python:3.12-slim` as its base image. The Dockerfile installs dependencies from `requirements.txt`, copies the Flask application into the image, and starts the application on port 5000.

### Build the image

```bash
sudo docker build -t devops-mini-project:1.0 .
```

### Run the container

```bash
sudo docker run -d \
  --name devops-mini-container \
  -p 5000:5000 \
  devops-mini-project:1.0
```

### Check the running container

```bash
sudo docker ps
```

### View application logs

```bash
sudo docker logs devops-mini-container
```

### Test the endpoints

```bash
curl -i http://localhost:5000/
curl -i http://localhost:5000/health
```

The homepage and health endpoint were verified successfully, returning HTTP 200 responses.

## 6. Automated Testing

Run the Python tests locally:

```bash
python -m pytest -v
```

**Verified result:** 2 tests passed.

The tests validate the homepage response and the health endpoint.

## 7. GitHub Actions CI

The workflow is defined in `.github/workflows/ci.yml`. It runs on pushes and pull requests targeting the `main` branch.

The workflow contains two jobs:

1. **Python tests:** Installs dependencies and executes pytest.
2. **Docker build:** Builds the application image using the Dockerfile.

Both jobs completed successfully in GitHub Actions.

The workflow builds the Docker image but does not publish it to a container registry or deploy the application.

## 8. Completed Work

- Flask application implemented and tested.
- Docker Engine installed and verified in Ubuntu WSL.
- Docker image built successfully.
- Container started and application endpoints verified.
- GitHub Actions Python test and Docker build jobs passed.

## 9. Future Improvements

- Improve container security and use Gunicorn for production-style serving.
- Add a Docker health check.
- Publish versioned images to Docker Hub.
- Deploy the application to a Linux server or cloud environment.
- Add monitoring and deployment verification.
