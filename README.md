# Environment Variables & Secrets

In any software project, certain values—like database credentials or API keys—can change based on the environment (development, testing, production). To handle this gracefully, we use **environment variables**.

---

## Environment Variables

Environment variables allow us to configure the app without hardcoding sensitive or environment-specific data into the source code.

Common examples:

- `MONGODB_USERNAME`
- `MONGODB_PASSWORD`
- `MONGODB_DB_NAME`

> These values are injected into the app at runtime and are typically written in **UPPER_SNAKE_CASE**.

In **GitHub Actions**, these variables can be defined directly in the workflow or passed as secrets (recommended for sensitive data).

---

## Secrets

Some environment variables contain **sensitive information** like credentials or tokens. These should **never be hardcoded or exposed** in the repository. Instead, we store them as **GitHub Secrets**.

GitHub provides multiple options for managing secrets:

- **Repository-level secrets**  
  Go to your repository → Settings → Secrets → Actions → _New repository secret_
- **Organization-level secrets**  
  Available for all repositories under a GitHub organization

> Secrets added here will be available securely in your CI/CD workflows.

---

## Environments in GitHub

GitHub allows you to define **environments** like `development`, `staging`, or `production`, each with its own set of secrets and rules.

This is helpful when:

- You need different values for the same variable across environments  
  _(e.g., `MONGODB_PASSWORD` for `test` vs `prod`)_
- You want to enforce extra checks before deploying  
  _(e.g., required reviewers, wait timers, branch protection rules)_

In your GitHub Actions workflow YAML file, you can link a job to a specific environment using the `environment:` key:

```yaml
jobs:
  deploy:
    environment: production
