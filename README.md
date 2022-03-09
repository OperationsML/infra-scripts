# Infrastructure templates

The infra_scripts repo contains samples of cloudformation scripts used to set up automated training and deployment pipelines for ML projects.

## Train_v2
- This script sets up a ci pipeline that connects a gitlab repo to codepipeline for ml workflow execution upon triggering (code change, scheduling). The pipeline can also be triggered off of a separate model monitoring cloud function.

## Deploy_v3
- This script sets up a CICD pipeline for ML model deployment thats linked to an S3 bucket that MLFlow uses to store models. When a new model tar file is uploaded to the bucket, codepipeline pulls the file (contains model and metadata), copies the model and version to an elastic file system, installs the necessary python requirements, and performs a build where a stage-api is created through AWS Lambda and API Gateway (See fmops-template repo inference for an example). The staged api is tested, submitted for approval, and deployed once approved.