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
8. [Sources](#sources)
9. [License](#license)
10. [Contact](#contact)

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
├── service/
│   ├── __init__.py
│   ├── models.py
│   ├── routes.py
│   └── ...
├── tests/
│   ├── test_models.py
│   ├── test_routes.py
│   └── ...
├── features/
│   ├── steps/
│   ├── environment.py
│   └── ...
├── requirements.txt
├── config.py
└── ...
```

### Database :

PostgreSQL serves as the database, accessible through the connection URI specified in the environment variables.SQLAlchemy acts as the Object Relational Mapper (ORM) for interacting with the database. Integrated with Flask through Flask-SQLAlchemy, it provides an interface to create and manage database tables and perform CRUD (Create, Read, Update, Delete) operations with Python.
### Data Model (About the Customer Account Model)

The data model for our account catalog is designed to store essential information about each account available in our eCommerce application. Here's an overview of the main features of the data model:

- **Account Name**: The unique name of the account.
- **Description**: A brief description of the account to help users understand its features.
- **Category**: The category to which the account belongs, facilitating navigation and search for users.
- **Availability**: Indicates whether the account is currently available for purchase.
- **Price**: The price of the account.

This data model is designed to provide a flexible structure while ensuring that all necessary information is easily accessible for users of our application.

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

### Behavior Tests :

In one terminal, start the application using:

```bash
honcho start
```

In another terminal, execute the BDD scenarios with:

```bash
behave
```

Ensure there are seven scenarios (Read, Update, Delete an Account, List all Accounts, List by Category, List by Available, List by Name) and that all pass.


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
git clone https://github.com/ibm-developer-skills-network/xgcyk-tdd-bdd-final-project-template.git
```

2. Navigate to the project directory:

```bash
cd xgcyk-tdd-bdd-final-project-template
```

3. Build the Docker image:

```bash
docker build -t account-catalog .
```

4. Run the Docker container:

```bash
docker run -d -p 5000:5000 --name account-catalog account-catalog
```

## Sources <a name="source"></a>

- **Template : [ibm-developer-skills-network/aolwx-devops-capstone-template](https://github.com/ibm-developer-skills-network/aolwx-devops-capstone-template)**
- **Useful links** :

  - **[DevOps Capstone Project](https://www.coursera.org/learn/devops-capstone-project/home/week/1)**

  - **[IBM DevOps and Software Engineering Professional Certificate](https://www.coursera.org/professional-certificates/devops-and-software-engineering)**

## License <a name="license"></a>

This project is licensed under the MIT License. See the `LICENSE` file for more information.

## Contact <a name="contact"></a>

### Contact Information :

- Send me email : **fkanecloudtech@gmailcom**
- Connect with me on [LinkedIn](https://www.linkedin.com/in/your-profile/)
- Visit my [portfolio](https://yourname.github.io) to explore my projects and services.


### Contribution and Support :

Contributions are welcome. Please refer to the `CONTRIBUTING.md` file for more information on how to contribute.

# SOURCES

**Github : [ibm-developer-skills-network/aolwx-devops-capstone-template](https://github.com/ibm-developer-skills-network/aolwx-devops-capstone-template)**
## Coursera links :

**Course : [DevOps Capstone Project](https://www.coursera.org/learn/devops-capstone-project/home/week/1)**

**Module : [Week 1 : Capstone Overview](https://www.coursera.org/learn/devops-capstone-project/supplement/wlYVl/capstone-overview)**

**Specialization : [IBM DevOps and Software Engineering Professional Certificate](https://www.coursera.org/professional-certificates/devops-and-software-engineering)**
