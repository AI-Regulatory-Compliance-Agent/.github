# Contributing to ComplianceAI

Thank you for your interest in contributing to ComplianceAI! This document provides guidelines and instructions for contributing to any repository in the organization.

---

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Repository Structure](#repository-structure)
- [Making Changes](#making-changes)
- [Commit Convention](#commit-convention)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)
- [Reporting Issues](#reporting-issues)

---

## Code of Conduct

By participating in this project, you agree to abide by our [Code of Conduct](CODE_OF_CONDUCT.md). Please read it before contributing.

---

## Getting Started

### Prerequisites

- **Docker** and **Docker Compose** (for running the full stack)
- **Python 3.11+** (for backend and ingestion development)
- **Node.js 20+** (for frontend development)
- **Git** (obviously 😄)

### Fork & Clone

1. Fork the repository you want to contribute to
2. Clone your fork locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/REPO_NAME.git
   cd REPO_NAME
   ```
3. Add the upstream remote:
   ```bash
   git remote add upstream https://github.com/AI-Regulatory-Compliance-Agent/REPO_NAME.git
   ```

---

## Development Setup

### Full Stack (Recommended)

```bash
# Clone all repos into a parent directory
mkdir complianceai && cd complianceai
git clone <org>/backend
git clone <org>/frontend
git clone <org>/ingestion
git clone <org>/Infrastructure

# Configure environment
cd Infrastructure
cp .env.example .env
# Edit .env with your credentials

# Launch the stack
docker compose up --build
```

### Backend Only

```bash
cd backend
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install torch --index-url https://download.pytorch.org/whl/cpu
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```

### Frontend Only

```bash
cd frontend
npm install
npm run dev
```

---

## Repository Structure

| Repository | Language | Description |
|-----------|----------|-------------|
| `backend` | Python | FastAPI + LangGraph agent pipeline |
| `frontend` | JavaScript | React + Vite dashboard |
| `ingestion` | Python | PDF → vector embedding pipeline |
| `Infrastructure` | YAML | Docker Compose + environment config |
| `.github` | Markdown | Organization templates & workflows |

---

## Making Changes

### Branch Naming

Use descriptive branch names with prefixes:

```
feature/add-new-regulation-parser
fix/sse-connection-timeout
docs/update-api-endpoints
refactor/simplify-agent-state
```

### Development Workflow

1. **Create a branch** from `main`:
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes** — keep commits focused and atomic

3. **Test your changes** locally:
   - Backend: Ensure the API starts and endpoints respond
   - Frontend: Verify the UI renders correctly
   - Ingestion: Test with a sample PDF

4. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```

5. **Open a Pull Request** against `main`

---

## Commit Convention

We follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

### Types

| Type | Description |
|------|-------------|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation changes |
| `style` | Code style changes (formatting, no logic change) |
| `refactor` | Code refactoring (no feature/fix) |
| `test` | Adding or updating tests |
| `chore` | Build process, dependency updates, etc. |
| `ci` | CI/CD configuration changes |

### Examples

```
feat(agents): add confidence calibration to risk scoring
fix(sse): resolve connection timeout on slow analyses
docs(readme): add API endpoint documentation
refactor(models): simplify company profile schema
```

---

## Pull Request Process

1. **Fill out the PR template** completely
2. **Ensure your branch is up to date** with `main`:
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```
3. **Describe the change** clearly in the PR description
4. **Link related issues** using `Closes #123` or `Fixes #456`
5. **Wait for review** — maintainers will review and may request changes
6. **Address feedback** with additional commits (don't force-push during review)

### PR Checklist

- [ ] Code follows the project's style guidelines
- [ ] Self-reviewed the code changes
- [ ] Added comments for complex logic
- [ ] Updated documentation if needed
- [ ] No new warnings or errors introduced
- [ ] Tested locally with Docker Compose

---

## Coding Standards

### Python (Backend & Ingestion)

- **Style**: PEP 8
- **Type hints**: Use them for function signatures
- **Docstrings**: Use triple-quote docstrings for modules, classes, and functions
- **Imports**: Standard library → third-party → local, separated by blank lines
- **Comments**: Explain *why*, not *what* — the code should be self-documenting

### JavaScript (Frontend)

- **Style**: ESLint configuration in `eslint.config.js`
- **Components**: Functional components with hooks
- **Naming**: PascalCase for components, camelCase for variables/functions
- **CSS**: Vanilla CSS with CSS custom properties (no utility frameworks)

### Docker

- **Base images**: Use `-slim` or `-alpine` variants
- **Layer caching**: Copy dependency files before source code
- **Security**: Don't include secrets in Dockerfiles

---

## Reporting Issues

### Bug Reports

Use the [Bug Report template](.github/ISSUE_TEMPLATE/bug_report.md) and include:
- Steps to reproduce
- Expected behavior
- Actual behavior
- Environment details (OS, Docker version, browser)
- Logs or screenshots

### Feature Requests

Use the [Feature Request template](.github/ISSUE_TEMPLATE/feature_request.md) and include:
- Problem description
- Proposed solution
- Alternative approaches considered
- Impact assessment

### Security Vulnerabilities

**Do NOT open a public issue.** Please follow our [Security Policy](SECURITY.md) for responsible disclosure.

---

## 💡 Need Help?

- Check the README of the relevant repository for specific setup instructions
- Look through existing issues for similar questions
- Open a new issue with the `question` label

Thank you for contributing to ComplianceAI! 🎉
