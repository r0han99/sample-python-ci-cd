# sample-python-ci-cd
An attempt to learn CI/CD

---
# Project Setup

## Repository Creation

1. A new GitHub repository named `sample-python-ci-cd` is created to host the project code.
2. The repository is cloned to the local machine.

## Project Structure

1. A basic directory structure is created with the main application file (`app.py`) and a test file (`test_app.py`).
2. `app.py` contains a simple function (`add`) and a script to print the result of adding two numbers.
3. `test_app.py` contains unit tests to verify the functionality of the `add` function using Python's `unittest` framework.
4. A `requirements.txt` file is created to list any dependencies needed for the project (empty in this case).

## CI (Continuous Integration) Setup with GitHub Actions

### Workflow Definition

1. A GitHub Actions workflow file named `ci.yml` is created in the `.github/workflows` directory.
2. The workflow is configured to run on every `push` and `pull_request` event to the `main` branch.

### Job Setup

1. The workflow defines a job named `build` that runs on an `ubuntu-latest` virtual machine.

### Steps in the Job

1. **Checkout Code:** Uses the `actions/checkout` action to check out the repository code.
2. **Set up Python:** Uses the `actions/setup-python` action to set up a specified version of Python (3.x).
3. **Install Dependencies:** Installs project dependencies using pip by reading the `requirements.txt` file.
4. **Run Tests:** Runs the unit tests using `unittest` to ensure the code is functioning correctly.

## CD (Continuous Deployment) Setup with Heroku

### Heroku Deployment

1. A `Procfile` is created to specify the command to run the application on Heroku (`web: python app.py`).

### Heroku App Creation

1. A Heroku app named `sample-python-ci-cd` is created using the Heroku CLI.
2. A remote Git repository for Heroku is added to the local Git configuration.

### GitHub Actions Deployment Step

1. The CI workflow file (`ci.yml`) is updated to include a deployment job named `deploy`.
2. The `deploy` job runs only if the `build` job succeeds, ensuring that only code that passes the tests is deployed.
3. **Checkout Code:** Uses the `actions/checkout` action again to check out the repository code.
4. **Deploy to Heroku:** Uses the Heroku API key stored in GitHub Secrets to push the code to Heroku for deployment.

### Secrets Configuration

1. The Heroku API key is added to the GitHub repository secrets to securely authenticate the deployment process.
