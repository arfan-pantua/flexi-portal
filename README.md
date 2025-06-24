## Portal/Frontend Application

This repository contains the source code for the Flexi Dev Portal and a GitHub Actions workflow for automated deployment to Azure App Service using a Docker container. The pipeline builds, tags, pushes a Docker image, and deploys it to Azure upon merging pull requests to the main branch.

## Prerequisites

To set up and run the pipeline, ensure the following:
- Docker Hub Account
- Azure Subscription

## How the Pipeline is Triggered
The pipeline is triggered automatically when:
- A pull request targeting the main branch is merged (i.e., closed with merged == true).
- The workflow listens for the pull_request_target event with the closed type on the main branch.

## Branch Protection Rules
To ensure code quality and security, the main branch is protected with the following rules, which must be configured in the repository settings:
- Require Pull Request Reviews:
    - At least one review from a code owner is required before merging.
    - Code owners are defined in a CODEOWNERS file (e.g., .github/CODEOWNERS).
- Require Status Checks to Pass:
    - Ensure all status checks (e.g., pipeline runs or other checks) pass before merging.
- Restrict Pushes:
    - Only allow merges via pull requests; direct pushes to main are blocked.

## Question
*How to rollback a deployment? How easy it is?*
There is no scenarion roll back on this Github Action, you need to create new branch and pull request to main. My suggestion is using deployment tool like Argocd to easy rollback

*Can we take the image deployed in production environment and deploy it into test
environment and will still works?*
You can't since this CICD processing is only support for one environment either production or development/test