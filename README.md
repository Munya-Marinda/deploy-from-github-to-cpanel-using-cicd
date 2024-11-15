# Deploy from GitHub to cPanel using CICD - Medium

This repository demonstrates how to set up Continuous Integration and Continuous Deployment (CICD) to deploy your website from GitHub to a cPanel server automatically whenever changes are pushed to the `main` branch.

## Table of Contents

- [Overview](#overview)
- [Setup Instructions](#setup-instructions)
- [Workflow Explanation](#workflow-explanation)
- [Sample Code](#sample-code)
- [Secrets Configuration](#secrets-configuration)
- [License](#license)

---

## Overview

This project provides:

- An example of using GitHub Actions for automating FTP deployments.
- A simple HTML template to use as an example website.

---

## Setup Instructions

### Step 1: Clone the Repository

Clone the repository to your local machine:

```bash
git clone https://github.com/<your-username>/deploy-from-github-to-cpanel-using-cicd.git
```

### Step 2: Add Your HTML Files

Replace the `index.html` file in the repository with your actual website content.

### Step 3: Set Up GitHub Secrets

1. Navigate to your GitHub repository.
2. Go to **Settings > Secrets and variables > Actions > New repository secret**.
3. Add the following secrets:
   - `FTP_HOST`: The FTP host (e.g., `ftp.yourdomain.com`).
   - `FTP_USERNAME`: The FTP username.
   - `FTP_PASSWORD`: The FTP password.
   - `FTP_DIR`: The directory on your server where the files should be uploaded (e.g., `/public_html`).

### Step 4: Push Changes

Push your code to the `main` branch, and GitHub Actions will handle the deployment automatically.

---

## Workflow Explanation

The GitHub Actions workflow (`.github/workflows/master.yml`) performs the following steps:

1. **Trigger on Push**: The workflow is triggered whenever changes are pushed to the `main` branch.
2. **Checkout Code**: Retrieves the latest code from the repository.
3. **Sync Files**: Uses the `SamKirkland/FTP-Deploy-Action` to deploy files via FTP.

### Workflow File

```yaml
name: Deploy Website

on:
  push:
    branches:
      - main

jobs:
  web-deploy:
    name: Deploying to Production

    runs-on: ubuntu-latest

    steps:
      - name: Get latest code
        uses: actions/checkout@v2

      - name: Sync files
        uses: SamKirkland/FTP-Deploy-Action@4.1.0
        with:
          server: ${{ secrets.FTP_HOST }}
          username: ${{ secrets.FTP_USERNAME }}
          password: ${{ secrets.FTP_PASSWORD }}
          server-dir: ${{ secrets.FTP_DIR }}
```

---

## Sample Code

### `index.html`

A basic HTML file to serve as the project's homepage:

---

## Secrets Configuration

The deployment relies on the following secrets:

- `FTP_HOST`: FTP server address.
- `FTP_USERNAME`: FTP login username.
- `FTP_PASSWORD`: FTP login password.
- `FTP_DIR`: Target directory on the FTP server.

Set these in your repository under **Settings > Secrets and variables > Actions**.

---

## License

This project is licensed under the MIT License. Feel free to use and modify it as needed.

---

## Author

Created by [Your Name](https://github.com/<Munya-Marinda). Follow me on GitHub for more projects like this.
