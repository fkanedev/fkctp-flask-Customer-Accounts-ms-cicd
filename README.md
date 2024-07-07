![Python](https://img.shields.io/badge/Python-3.8-blue.svg)
![Flask](https://img.shields.io/badge/Flask-2.2.3-b5f05d.svg)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-2.0.0-orange.svg)
![Factory Boy](https://img.shields.io/badge/Factory--Boy-3.2.1-brightgreen.svg)
![Powered by PostgreSQL](https://img.shields.io/badge/Powered%20by-PostgreSQL-336791.svg)
![Coverage Status](https://img.shields.io/badge/Coverage-95%25-green)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

# Customer Account Microservice

This project involves the development of a microservice for managing customer accounts using Test Driven Development (TDD). I undertook this project as part of my training in the [IBM DevOps and Software Engineering Professional Certificate](https://www.coursera.org/professional-certificates/devops-and-software-engineering). It highlights the practical application of skills such as TDD, Continuous Integration (CI), Continuous Deployment (CD), security headers and cross-origin resource sharing (CORS) policies, acquired during the training. To achieve this, I used [this template](https://github.com/ibm-developer-skills-network/aolwx-devops-capstone-template) provided by IBM Developer Skills Network.

## Table of Contents

1. [Introduction](#introduction)
2. [Technologies Used](#technologies-used)
3. [Installation and Configuration](#installation-configuration)
4. [Usage](#usage)
5. [Development](#development)
6. [Testing](#testing)
7. [Deployment](#deployment)
8. [CI/CD Pipeline](#ci-cd-pipeline)
9. [Security](#security)
10. [Sources](#sources)
11. [License](#license)
12. [Contact](#contact)

## Introduction <a name="introduction"></a>

### Project Objective :
This project aims to create a RESTful Flask microservice for managing customer accounts. The microservice will implement test cases for CRUD functions and ensure they pass these tests, add security headers and CORS policies with Flask-Talisman and Flask-Cors, integrate a CI pipeline with GitHub Actions, and a CD pipeline with Tekton and OpenShift.

### Key Features :

- Create, read, update, delete, and list accounts.
- Apply some secure code practices: security headers and CORS policies.

## Technologies Used <a name="technologies-used"></a>

### Programming Languages :

- Python 3.8

### Tools and Frameworks :

- Flask (for the REST API microservice)
- Flask-Talisman (for security headers)
- Flask-Cors (for CORS policies)
- Nose (for TDD)
- factory-boy (for creating test data)

## Installation and Configuration <a name="installation-configuration"></a>

### Prerequisites :

- Python 3.8
- pip (Python package manager)

### Installation Steps :

1. Clone the GitHub repository:

```bash
git clone https://github.com/fkanedev/fkctp-flask-Customer-Accounts-ms-cicd
cd fkctp-flask-Customer-Accounts-ms-cicd
```

2. Create and activate a virtual environment:

```bash
python3.8 -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```

3. Install the dependencies:

```bash
pip install -r requirements.txt
```

### Environment Configuration :

Ensure the Python environment is properly set up with Python 3.8. Dependencies should be installed via `pip`.

### Environment Variables :

- `FLASK_ENV=development`
- Other required configuration items are already defined in the [service/config.py](https://github.com/fkanedev/fkctp-flask-Customer-Accounts-ms-cicd/blob/main/service/config.py) file.

## Usage <a name="usage"></a>

### Usage Instructions :

To start the application, use the following command:

```bash
flask run
```

### Use Case Examples :

- **Create an account:**
To create an account, send a POST request to the `/accounts` endpoint with the account details in the request body.

```bash
curl -i -X POST http://127.0.0.1:5000/accounts \
-H "Content-Type: application/json" \
-d '{"name":"John Doe","email":"john@doe.com","address":"123 Main St.","phone_number":"555-1212"}'
```

- **Read an account:**
To read an account, send a GET request to the `/accounts/<account_id>` endpoint with the account ID.

```bash
curl -i -X GET http://127.0.0.1:5000/accounts/1
```

- **Update an account:**
To update an account, send a PUT request to the `/accounts/<account_id>` endpoint with the updated account details in the request body.

```bash
curl -i -X PUT http://127.0.0.1:5000/accounts/1 \
-H "Content-Type: application/json" \
-d '{"name":"John Doe","email":"john@doe.com","address":"123 Main St.","phone_number":"555-1111"}'
```

- **Delete an account:**
To delete an account, send a DELETE request to the `/accounts/<account_id>` endpoint with the account ID.

```bash
curl -X DELETE http://localhost:5000/accounts/1
```

- **List all accounts:**
To list all accounts, send a GET request to the `/accounts` endpoint.

```bash
curl -i -X GET http://127.0.0.1:5000/accounts
```

## Development <a name="development"></a>

### Project Structure :

This backend project is primarily organized around the Flask framework. The directory structure includes the following folders:
- `service`: Contains routes and data models.
- `tests`: Contains unit tests and integration tests.
- `features`: Contains BDD scenarios and associated steps.

```plaintext
.
├── github/
│   └── workflows/
│   │   └── ci-buil.yml
│   └── ...
├── deploy/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ...
├── service/
│   ├── common/
│   ├── models.py
│   ├── routes.py
│   └── ...
├── tekton/
│   ├── pipeline.yaml
│   ├── pvc.yaml
│   └── tasks.yaml
├── tests/
│   ├── factories.py
│   ├── test_models.py
│   ├── test_routes.py
│   └── ...
├── README.md
├── requirements.txt
└── ...
```

### Database :

PostgreSQL serves as the database, accessible through the connection URI specified in the environment variables.SQLAlchemy acts as the Object Relational Mapper (ORM) for interacting with the database. Integrated with Flask through Flask-SQLAlchemy, it provides an interface to create and manage database tables and perform CRUD (Create, Read, Update, Delete) operations with Python.
### Data Model (About the Customer Account Model)

The data model for our customer account is designed to store essential information about each customer registred with the microservice in the database. Here's an overview of the main features of the data model:

| Name | Type | Optional |
|------|------|----------|
| id | Integer| False |
| name | String(64) | False |
| email | String(64) | False |
| address | String(256) | False |
| phone_number | String(32) | True |
| date_joined | Date | False |

## Testing <a name="testing"></a>

The TDD and BDD techniques implemented in this project ensure the most comprehensive testing possible and the maintenance of high code coverage. To verify this, you can follow the steps outlined below. 

### Unit Tests :

Execute the following command to run the unit tests and measure code coverage. Ensure the project maintains at least 95% code coverage:

```bash
nosetests --with-coverage --cover-erase --cover-package=service
```

- `--with-coverage`: Activates the coverage plugin.
- `--cover-erase`: Clears previous coverage data.
- `--cover-package=service`: Measures coverage for the service package only.

## Deployment <a name="deployment"></a>

This project supports both manual deployment and containerized deployment using Docker. Below are the detailed instructions for each method.

### Manual Deployment :

The manual deployment strategy involves directly setting up the environment and running the application on the host machine. This method is simple and suitable for small-scale deployments or development purposes. However, it requires manual setup and is less scalable for larger applications.

1. Clone the repository:

```bash
git clone https://github.com/ibm-developer-skills-network/xgcyk-tdd-bdd-final-project-template.git
```

2. Navigate to the project directory:

```bash
cd xgcyk-tdd-bdd-final-project-template
```

3. Set the environment to production:

```bash
export FLASK_ENV=production
```

4. Install the required dependencies:

```bash
pip install -r requirements.txt
```

5. Run the application:

```bash
flask run
```

### Containerized Deployment :

The containerized deployment strategy involves packaging the application and its dependencies into a Docker container. This ensures consistency and portability across different environments. Docker containers can be easily managed, scaled, and deployed on various platforms, making this method efficient for both development and production environments.

1. Clone the repository:

```bash
git clone https://github.com/fkanedev/fkctp-flask-Customer-Accounts-ms-cicd
```

2. Navigate to the project directory:

```bash
cd fkctp-flask-Customer-Accounts-ms-cicd
```

3. Build the Docker image:

```bash
docker build -t accounts .
```

4. Run the Docker container:

```bash
docker run -d -p 5000:5000 --name accounts accounts
```

### Deploy to Kubernetes :

The following steps were undertaken to deploy the application to Kubernetes:

1. **Set up Kubernetes Cluster:**
   - Provisioned a Kubernetes cluster using a suitable cloud provider.

2. **Create Docker Image:**
   - Built and pushed the application's Docker image to a container registry (e.g., Docker Hub).

3. **Create Kubernetes Deployment:**
   - Defined a Kubernetes Deployment YAML file ([deployment.yaml](https://github.com/fkanedev/fkctp-flask-Customer-Accounts-ms-cicd/blob/main/deploy/deployment.yaml)) and applied its configuration to the cluster.

4. **Create Kubernetes Service:**
   - Defined a Kubernetes Service YAML file ([service.yaml](https://github.com/fkanedev/fkctp-flask-Customer-Accounts-ms-cicd/blob/main/deploy/service.yaml)) and applied its configuration to the cluster.

5. **Verify Deployment:**
   - Verified the application’s deployment by checking pod and service statuses.
   - Accessed the application using its service endpoint to ensure successful deployment.


## CI/CD Pipeline <a name="ci-cd-pipeline"></a>

### Continuous Integration (CI) with GitHub Actions

The codebase comes with unit tests for the provided endpoints. The goal is to set up CI pipelines using GitHub Actions to automate the linting and testing processes. To achieve this, we create a GitHub Actions workflow that triggers whenever changes are pushed to the repository.

Check the content of the [`github/workflows/workflow.yml`](https://github.com/fkanedev/fkctp-flask-Customer-Accounts-ms-cicd/blob/main/.github/workflows/ci-build.yml) file for the CI pipeline definition. Initially, the workflow sets up the PostgreSQL service using the postgres:alpine image to create a database instance. This setup includes configuring the database with a password and a test database, and verifying the service's health before proceeding to the build steps. 
Next, the workflow performs several steps:

- **Checkout:** Uses the GitHub Action to check out the repository.
- **Install dependencies:** Installs the necessary Python dependencies listed in `requirements.txt`.
- **Lint with flake8:** Runs `flake8` to ensure code quality and check for syntax errors.
- **Run unit tests with nose:** Executes unit tests using `nose` with detailed reporting and coverage information.

You can verify the success of the workflows by checking the "build passing" badge at the beginning of the README or by navigating to the "Actions" tab in the GitHub repository to see detailed execution logs.

## Continuous Deployment (CD)

### Build an Automated CD DevOps Pipeline Using Tekton and OpenShift

The following steps were undertaken to build an automated CD DevOps pipeline using Tekton and OpenShift:

1. **Create a Tekton Pipeline:**
   - Defined tasks and pipeline resources in YAML files: [tekton/pvc.yaml](https://github.com/fkanedev/fkctp-flask-Customer-Accounts-ms-cicd/blob/main/tekton/pvc.yaml), [tekton/tasks.yaml](https://github.com/fkanedev/fkctp-flask-Customer-Accounts-ms-cicd/blob/main/tekton/tasks.yaml) and [tekton/pipeline.yaml](https://github.com/fkanedev/fkctp-flask-Customer-Accounts-ms-cicd/blob/main/tekton/pipeline.yaml).

2. **Install Tekton CLI (tkn):**
   - Used `tkn` for managing pipelines.

3. **Create and add tasks for CD Pipeline a Build Task:**
   - Lint task (flake8) linter.
   - Tests task (Nose) to run unit tests with PyUnit.
   - Added a Tekton Build Task (buildah) to build the application: included steps to clone the repository and build the Docker image.

4. **Create a Deployment Task:**
   - Wrote a Tekton task to deploy the application.
   - Used `kubectl` commands within the task to deploy to Kubernetes.

5. **Create an Image Resource:**
   - Defined an image resource for the output.
   - Specified the target container registry.

6. **Create a Pipeline:**
   - Combined tasks into a pipeline definition.
   - Linked tasks using pipeline resources.
   - Run the Pipeline using Tekton CLI.

7. **Monitor Pipeline Runs:**
   - Used `tkn` to monitor the status of pipeline runs.
   - Checked logs for each task to debug issues.

## Security <a name="security"></a>

To enhance the security of the application, the following practices were implemented:

- Security Headers:

  - Utilized Flask-Talisman to set HTTP security headers.
  - Configured headers like :
    - Content Security Policy (CSP),
    - Strict-Transport-Security (HSTS),
    - X-Content-Type-Options,
    - X-Frame-Options,
    - Referrer-Policy
    to mitigate various web vulnerabilities. Together, they enhance security by protecting against XSS (Cross-Site Scripting) attacks, ensuring secure usage of HTTPS connections, preventing MIME-sniffing and clickjacking attacks and controlling the disclosure of referrer information.

- CORS Policies:

  - Integrated Flask-CORS to handle Cross-Origin Resource Sharing (CORS) policies.
  - Configured CORS to allow or restrict resources based on the client's origin, ensuring that only trusted domains can interact with the APIs.

These measures help protect against common web security threats and ensure that the application adheres to best practices for secure code.
## Sources <a name="source"></a>

- **Template : [ibm-developer-skills-network/aolwx-devops-capstone-template](https://github.com/ibm-developer-skills-network/aolwx-devops-capstone-template)**
- **Useful links** :

  - **[DevOps Capstone Project](https://www.coursera.org/learn/devops-capstone-project/home/week/1)**

  - **[IBM DevOps and Software Engineering Professional Certificate](https://www.coursera.org/professional-certificates/devops-and-software-engineering)**

## License <a name="license"></a>

This project is licensed under the MIT License. See the `LICENSE` file for more information.

## Contact <a name="contact"></a>

### Contact Information :

- Send me email : **fkanecloudtech@gmail.com**
- Connect with me on [LinkedIn](https://www.linkedin.com/in/your-profile/)
- Visit my [portfolio](https://yourname.github.io) to explore my projects and services.


### Contribution and Support :

Contributions are welcome. Please refer to the `CONTRIBUTING.md` file for more information on how to contribute.
