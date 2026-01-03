# Azure Web App CI/CD with GitHub Actions

This project demonstrates an end-to-end CI/CD pipeline that automatically deploys a simple web application to **Azure App Service** whenever code is pushed to the `main` branch.

## What this project does
- Hosts a web app on **Azure App Service**
- Uses **GitHub Actions** to automate deployment
- Deploys on every push to `main` (CI/CD)

## Tech Stack
- **Azure App Service (Web App)**
- **GitHub Actions**
- **ZIP Deploy (OneDeploy via Kudu/SCM)**

## Architecture (high level)
Developer push → GitHub repo → GitHub Actions workflow → Azure App Service

## CI/CD Workflow
On push to `main`, the pipeline:
1. Checks out the repository
2. Packages the site into a ZIP file
3. Deploys the ZIP to Azure Web App using `azure/webapps-deploy`

Workflow file: `.github/workflows/deploy.yml`

## Setup Summary
### Azure
1. Create an **App Service Plan**
2. Create an **Azure Web App**
3. Configure deployment access (Publish Profile / or OIDC in future)

### GitHub
1. Add repository secrets:
   - `AZURE_WEBAPP_NAME` = `<your-webapp-name>`
   - `AZURE_WEBAPP_PUBLISH_PROFILE` = Publish Profile XML (stored securely as a GitHub Secret)
2. Push changes to `main` to trigger deployment

## How to Run
1. Clone the repo
2. Update `index.html` (or any content)
3. Push to `main`
4. Check GitHub → **Actions** for a successful run
5. Verify the live site: **<YOUR_WEB_APP_URL>**

## Screenshots
Add your screenshots in the `/screenshots` folder and reference them here.

- GitHub Actions successful run:
  - `screenshots/github-actions-success.png`
- Azure App Service overview:
  - `screenshots/azure-app-service-overview.png`
- Live website:
  - `screenshots/live-site.png`

## Troubleshooting Notes (real-world)
- **Git push rejected (non-fast-forward):** fixed by pulling remote changes before pushing (`git pull --rebase`).
- **Publish profile download blocked:** occurs if SCM basic auth publishing credentials are disabled. Temporarily enabled to download the profile, then disabled again for security.
- **401 Unauthorized during deploy:** typically caused by incorrect publish profile secret or SCM credential settings.

## Next Improvements (Roadmap)
- Replace publish profile authentication with **OIDC (Federated Credentials)** for stronger security
- Provision Azure resources using **Terraform/Bicep** (Infrastructure as Code)
- Add environment protection and approvals (Dev/Test/Prod)

## Author
Rambabu Katta  
This project is part of my Azure Cloud Engineering learning journey to build hands-on, job-ready projects.
