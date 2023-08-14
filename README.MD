# GitHub Actions Deep Dive

A simple Lambda function that can be deployed via a GitHub Actions Workflow. 

# Deploy my Lambda Function Workflow

This repository contains a GitHub Actions workflow that automates the deployment of a Lambda function using AWS services. The workflow triggers on all push events to the `main` branch. It performs linting, building, uploading to S3, and deploying to AWS Lambda.

## Workflow Steps

The workflow consists of the following steps:

### 1. Linting (`lint` job)

This job performs linting on the function code using `flake8` to ensure code quality.

### 2. Build and Create Zip Bundle (`build` job)

In this step, the function dependencies are installed, and a zip bundle is created for the Lambda function code. The zip bundle is then uploaded as an artifact.

### 3. Upload to S3 (`upload` job)

The zip bundle artifact is downloaded from the previous step and uploaded to an S3 bucket for storage.

### 4. Non-Prod Testing (`nonprod` job)

This job creates a Lambda function from the uploaded code, invokes the function with different inputs for testing, and then deletes the test function.

### 5. Deploy to Lambda (`deploy` job)

The final step updates the Lambda function code with the latest version from the S3 bucket, effectively deploying the function to AWS Lambda.

## Usage

1. Clone this repository to your local machine:

```bash
git clone https://github.com/your-username/deploy-lambda-function.git
cd deploy-lambda-function

Modify the workflow file (.github/workflows/main.yml) as needed, adjusting environment variables, input parameters, and other configuration details.

Create AWS credentials secrets in your GitHub repository settings. The required secrets are AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_REGION, and AWS_ACCOUNT_ID.

Make any necessary changes to your Lambda function code in the function directory.

Commit and push your changes to the main branch to trigger the workflow.

Workflow Customization
You can customize this workflow to suit your specific needs by modifying the workflow file. Additionally, you can add more jobs or steps to the workflow to include additional testing, notifications, or other actions.
