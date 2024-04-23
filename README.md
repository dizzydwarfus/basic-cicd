## Deployment Process for Django Application to AWS Elastic Beanstalk

This guide outlines the steps to deploy a Django application to AWS Elastic Beanstalk using GitHub Actions.


@import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false}

<!-- code_chunk_output -->

- [Deployment Process for Django Application to AWS Elastic Beanstalk](#deployment-process-for-django-application-to-aws-elastic-beanstalk)
  - [Project Structure](#project-structure)
  - [GitHub Actions Workflow](#github-actions-workflow)
  - [Deployment Workflow Overview](#deployment-workflow-overview)
  - [Getting Started](#getting-started)
  - [Conclusion](#conclusion)

<!-- /code_chunk_output -->



### Project Structure
- **Django Project:** Contains your Django application code.
  - **core:** Django app containing views and tests.
  - **django_github_actions_aws:** Project directory containing settings, URLs, and WSGI configurations.
  - **manage.py:** Django's command-line utility for administrative tasks.
- **Other Files:**
  - **wsgi.py:** WSGI configuration exposing the WSGI callable as `application`.
  - **.ebextensions/ebconfiguration:** Configuration file for Elastic Beanstalk, specifying the WSGI path.

### GitHub Actions Workflow
- A GitHub Actions workflow is set up to automate the deployment process.
- The workflow consists of two main jobs: "test" and "deploy".
  - **test:** Runs unit tests to ensure the application works as expected.
  - **deploy:** Deploys the application to AWS Elastic Beanstalk after tests pass.

### Deployment Workflow Overview
1. **Test Job:**
   - Installs dependencies, including Python packages specified in `requirements.txt`.
   - Runs unit tests defined in `core/tests.py`.

2. **Deploy Job:**
   - Generates a deployment package by zipping the project directory.
   - Deploys the package to Elastic Beanstalk using the `einaregilsson/beanstalk-deploy` action.
     - Configurations such as application name, environment name, and AWS credentials are specified in GitHub Secrets.
     - The `deployment_package` is specified as `deploy.zip`.
     - Elastic Beanstalk's WSGI path is configured in `.ebextensions/ebconfiguration`.

### Getting Started
1. Ensure all necessary Django configurations are correctly set up in `settings.py`, including database and static file settings.
2. Test your Django application locally to verify it functions as expected.
3. Set up your AWS Elastic Beanstalk environment and obtain necessary IAM credentials.
4. Configure GitHub Secrets for AWS credentials in your repository settings.
5. Update the deployment workflow (`deploy.yml`) with your specific configurations (application name, environment name, etc.).
6. Push changes to your main branch to trigger the deployment workflow.
7. Monitor the GitHub Actions workflow to ensure successful deployment.
8. Check your Elastic Beanstalk environment for the deployed application.

### Conclusion
You have now automated the deployment process of your Django application to AWS Elastic Beanstalk using GitHub Actions. This allows for streamlined deployment and ensures consistency across environments.
