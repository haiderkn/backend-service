# backend-service

`backend-service` is a backend system built using Django Rest Framework. It is containerized with Docker, utilizes JWT for secure authentication, and relies on PostgreSQL as the database. The project is designed to run in production behind an Nginx server with deployment configured via Docker Compose. CI/CD is set up with GitHub Actions to automate testing, image versioning, and deployment to an AWS t2.micro instance.

## Key Features

- **Framework:** Django Rest Framework
- **Authentication:** JWT
- **Database:** PostgreSQL
- **Server:** Nginx
- **Containerization:** Docker
- **Deployment:** Docker Compose
- **Cloud server:** AWS instance

## CI/CD Pipeline

- **CI/CD Tool:** GitHub Actions
- **Image Storage:** Docker Hub (with versioning)
- **Tests:**
  - **Unit Tests:** Written using `unittest`
  - **Linter:** Code checked with `flake8`
  - **Code Quality:** Analyzed with GitHub CodeQL

## Deployment Process

1. **Trigger**: On push to the `main` branch.
2. **CI Steps**:
   - **Run Linter** (`flake8`)
   - **Execute Unit Tests** (`unittest`)
3. **Build and Push Image**: If all three test passes, GitHub Actions builds a Docker image, tags it with a version, and pushes it to Docker Hub.
4. **Deploy to AWS**:
   - GitHub Actions SSHs into an AWS t2.micro instance.
   - Pulls the latest Docker image from Docker Hub.
   - Runs the container on the AWS instance using a Docker Compose file.

## Local Development Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/haiderkn/backend-service.git
   cd backend-service
   ```

2. Start the containers with Docker Compose:
   ```bash
   docker compose -f docker-compose-localdev.yml up --build
   ```

3. Access the API at `http://localhost:<port>`.

## Running Tests Locally

1. **Unit Tests**:
   ```bash
   python manage.py test
   ```

2. **Linting**:
   ```bash
   flake8 .
   ```

## Deployment Architecture

- **Deployment Server**: AWS t2.micro instance
- **Method**: CI/CD workflow on merge to `main` runs linter and unit tests, builds and tags Docker image, pushes it to Docker Hub, SSHs into AWS, pulls the image, and deploys it with Docker Compose.

## Additional Information

For any queries or contributions, please open an issue or submit a pull request.

## Features to be added
- automate server setup using Ansible
