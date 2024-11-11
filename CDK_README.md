## AWS CDK Project with Python

This project demonstrates how to set up and deploy an AWS resource (S3 bucket) using AWS CDK with Python.

### Prerequisites
- Node.js: Make sure Node.js (>=14.x) is installed.
- AWS CLI: Ensure the AWS CLI is configured with your AWS credentials.
- Python 3.7+: CDK for Python requires Python 3.7 or newer.
- AWS CDK Toolkit: Install the AWS CDK Toolkit using npm or yarn: `npm install -

### Getting Started
1. Install AWS CDK:

```bash
npm install -g aws-cdk
```
2. Initialize CDK Project: Create a new directory for your project, navigate into it, and initialize a Python CDK app:

```bash
mkdir cdk_project
cd cdk_project
cdk init app --language python
```

3. Set Up Virtual Environment: Activate a virtual environment for Python dependencies:

```bash
# macOS/Linux
source .venv/bin/activate

# Windows
.venv\Scripts\activate
```
4. Install Required CDK Modules: After initialization, install the necessary AWS CDK libraries:

```bash
pip install -r requirements.txt
pip install aws-cdk-lib constructs
```
5. Define Your AWS Resources
Open the app.py file and update it to look like this:

```python
Copy code
# app.py
import aws_cdk as cdk
from cdk_project.cdk_project_stack import CdkProjectStack

app = cdk.App()
CdkProjectStack(app, "CdkProjectStack")
app.synth()
```
6. Open the cdk_project_stack.py file in the lib folder, and define an S3 bucket:

```python
# cdk_project_stack.py
from aws_cdk import Stack
from aws_cdk import aws_s3 as s3
from constructs import Construct

class CdkProjectStack(Stack):
    def __init__(self, scope: Construct, construct_id: str, **kwargs) -> None:
        super().__init__(scope, construct_id, **kwargs)

        # Define an S3 Bucket
        s3.Bucket(self, "MyBucket", versioned=True)

```

### Synthesizing the CloudFormation Template
To generate the CloudFormation template from your CDK code, run:

```bash
cdk synth
```
This command outputs a CloudFormation template in YAML format, which you can review before deployment.

### Deploying the Stack
To deploy the stack and create resources in your AWS account:

```bash
cdk deploy
```
CDK will ask for confirmation if there are resources that may incur charges.

### Viewing Resources in AWS Console
- S3 Bucket: Visit the S3 Console to see the created S3 bucket.

- CloudFormation Stack: Go to the CloudFormation Console to view the deployed stack and its resources.
Additional Notes
- AWS Credentials in VS Code: Use the AWS Toolkit in VS Code by going to the AWS Explorer panel and selecting “Connect to AWS” to authenticate.
- CDK Bootstrap: The CDK requires a bootstrap stack in each environment. Run cdk bootstrap if you encounter issues related to the bootstrap stack.

### Cleanup
To delete the resources created by this stack:

```bash
cdk destroy
```

### Useful Commands
- cdk synth – Synthesize the CloudFormation template.
- cdk deploy – Deploy the stack.
- cdk diff – Compare deployed stack with the local code.
- cdk destroy – Delete the stack and its resources.