---
description: Commit to GitHub and Deploy to Vercel
---
### Deployment Workflow

This workflow automates the process of creating a new GitHub repository, pushing the current code to it, and deploying the project to Vercel.

**Required Information from User:**
- Project Name (e.g., `proven-kitchen-bath-studio`)

**Steps:**

// turbo-all

1. Remove existing git repository (if any) to detach from the template.
```bash
rm -rf .git
```

2. Initialize a new git repository and make the initial commit.
```bash
git init
git add .
git commit -m "Initial commit for new client"
```

3. Create a new public GitHub repository and push the code. Replace `<project-name>` with the user-provided project name.
```bash
gh repo create <project-name> --public --source=. --remote=origin --push
```

4. Link the project to Vercel and deploy. Replace `<project-name>` with the user-provided project name.
```bash
vercel link --yes --project <project-name>
vercel deploy --prod
```
