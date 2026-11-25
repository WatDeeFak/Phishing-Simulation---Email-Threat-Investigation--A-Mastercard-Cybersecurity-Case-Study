# GitHub Upload Guide

This folder is prepared as a local repository package. It has not been published to GitHub.

## Create the remote repository

1. Sign in to GitHub and create a new repository.
2. Suggested name: `mastercard-phishing-investigation`.
3. Suggested description: `Fictional phishing investigation case study covering email authentication, URL and attachment analysis, evidence correlation, incident response, and security awareness.`
4. Choose Public only if you are comfortable publishing the fictional sample artefacts and presentation. Do not upload real company data, employee information, credentials, or production logs.
5. Upload the contents of this folder, keeping the directory structure intact.

## Verify before publishing

- Confirm that all domains are reserved example domains.
- Confirm that all IPs and hashes are explicitly marked as fictional training artefacts.
- Do not describe the 24 deliveries, three clicks, or 12.5% click rate as real employee results.
- Do not claim that a real Mastercard campaign, incident, or employee investigation was performed.
- Review the PowerPoint and image assets for any third-party template attribution requirements.

## Suggested repository settings

- Add topics: `phishing-analysis`, `email-security`, `soc-analysis`, `incident-response`, `threat-intelligence`, `security-awareness`, `forage-simulation`.
- Keep the README as the default landing page.
- If you later add genuine lab evidence, label its source and scope clearly and remove secrets or sensitive data before publishing.

## Optional Git command workflow

From a terminal opened in the extracted project folder:

```bash
git init
git add .
git commit -m "Add phishing investigation case study"
git branch -M main
git remote add origin https://github.com/USERNAME/mastercard-phishing-investigation.git
git push -u origin main
```

Replace `USERNAME` with your GitHub username. Create the empty remote repository first. Do not commit credentials or environment files.
