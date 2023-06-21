# Deploy to Google App Engine via Github Actions

0) Prerequisite: You have all GCP ready, and have already deployed to the app engine.

1) GCloud Setup - You need service account with following IAM roles (it might be too much, but it's good start)
- App Engine Admin
- App Engine Deployer
- Cloud Build Service Account
- Service Account User
- Storage Admin
Also you need to enable the App Engine Admin API, it is off by default.
Download the SA Json.

2) Create the github action as follows:

```
name: Deploy to GAE

# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  deploy:
    name: Deploying to Google Cloud
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout
      uses: actions/checkout@v2

    - name: Deploy to App Engine
      id: deploy
      uses: google-github-actions/deploy-appengine@v0.2.0
      with:
        deliverables: app.yaml
        version: v1
        project_id: ${{ secrets.GCP_PROJECT }}
        credentials: ${{ secrets.GCP_CREDENTIALS }}

    - name: Test
      run: curl "${{ steps.deploy.outputs.url }}"
```

3) Create 2 secrets in repo `GCP_PROJECT` and the `GCP_CREDENTIALS`. The SA Json value goes to `GCP_CREDENTIALS` and you should know how to get the project.

