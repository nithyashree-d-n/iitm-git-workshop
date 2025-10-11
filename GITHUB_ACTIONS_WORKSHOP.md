# GitHub Actions Workshop - CI/CD Pipeline Demo

This repository contains a simple GitHub Actions workflow designed for educational purposes to demonstrate key CI/CD concepts.

## 📋 What is GitHub Actions?

GitHub Actions is a continuous integration and continuous deployment (CI/CD) platform that allows you to automate your build, test, and deployment pipeline. You can create workflows that build and test every pull request to your repository, or deploy merged pull requests to production.

## 🔧 Workflow Overview

The workflow file is located at `.github/workflows/ci.yml` and demonstrates the following concepts:

### Triggers

```yaml
on:
  push:
    branches: [main, master]
  pull_request:
    branches: [main, master]
```

- **Push events**: Runs when code is pushed to main/master branch
- **Pull request events**: Runs when a PR is opened or updated

### Jobs Structure

Our workflow contains 3 jobs that showcase different execution patterns:

## 🏗️ Job 1: Build and Test

**Runs**: On every trigger
**Purpose**: Core CI functionality

### Steps:

1. **Checkout code** - Downloads repository content
2. **Setup Node.js** - Installs Node.js v18 with npm caching
3. **Install dependencies** - Runs `npm ci` for clean, reproducible builds
4. **Build project** - Executes `npm run build` to compile the Astro site
5. **Verify build output** - Checks that the `dist` folder was created successfully

### Key Learning Points:

- Using pre-built actions (`actions/checkout@v4`, `actions/setup-node@v4`)
- Dependency caching for faster builds
- Basic error handling and verification

## 🔍 Job 2: Code Quality

**Runs**: In parallel with Build job
**Purpose**: Demonstrate parallel execution and basic quality checks

### Steps:

1. **Environment setup** - Same as build job
2. **Project structure validation** - Verifies required files exist
3. **File type counting** - Shows project composition

### Key Learning Points:

- **Parallel execution**: Runs simultaneously with build job
- **Shell scripting**: Using bash commands for custom checks
- **Project analysis**: Automated quality validation

## 🚀 Job 3: Deploy Simulation

**Runs**: Only after build succeeds, only on main/master branch
**Purpose**: Show conditional execution and job dependencies

### Features:

- **Job dependency**: Uses `needs: build` to wait for build completion
- **Conditional execution**: Only runs on main/master branch
- **Simulation**: Demonstrates deployment concepts without actual deployment

### Key Learning Points:

- **Job dependencies**: Sequential execution with `needs`
- **Conditional logic**: Using `if` conditions
- **Environment variables**: Accessing GitHub context (`github.ref_name`, `github.sha`, etc.)

## 🎯 How to Test This Workflow

1. **Fork this repository** to your GitHub account
2. **Make any change** to a file (e.g., edit this README)
3. **Commit and push** to the main branch, or create a pull request
4. **Visit the Actions tab** in your GitHub repository to see the workflow run

## 📊 What You'll See

When the workflow runs, you'll observe:

- ✅ **Build job** compiling the Astro project
- ✅ **Code Quality job** running in parallel, analyzing the project structure
- ✅ **Deploy Simulation job** (only on main/master) showing deployment info
- 📈 **Real-time logs** for each step
- ⏱️ **Execution time** and resource usage
- 🔄 **Status indicators** (success, failure, in progress)

## 🎓 Learning Objectives

After studying this workflow, you should understand:

1. **Basic YAML syntax** for GitHub Actions
2. **Workflow triggers** and when jobs execute
3. **Job dependencies** and parallel vs sequential execution
4. **Using marketplace actions** vs writing custom commands
5. **Environment setup** and dependency management
6. **Conditional logic** in workflows
7. **Context and environment variables**
8. **Basic error handling** and verification steps

## 🔧 Customization Ideas

Try modifying the workflow to experiment:

- Add a **security scanning** job
- Include **automated testing** steps
- Add **artifact upload/download**
- Implement **matrix builds** for multiple Node.js versions
- Create **environment-specific deployments**
- Add **notification steps** (Slack, email, etc.)

## 📚 Next Steps

1. Explore the [GitHub Actions documentation](https://docs.github.com/en/actions)
2. Browse the [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)
3. Try creating your own workflow from scratch
4. Look into advanced features like:
   - Reusable workflows
   - Custom actions
   - Self-hosted runners
   - Secrets and environment variables

## ❓ Common Questions

**Q: Why use `npm ci` instead of `npm install`?**
A: `npm ci` is faster and more reliable for CI environments as it installs directly from package-lock.json.

**Q: What's the difference between `runs-on` options?**
A: `ubuntu-latest`, `windows-latest`, and `macos-latest` provide different operating system environments.

**Q: How do I see the workflow results?**
A: Go to your repository → Actions tab → Click on any workflow run to see detailed logs.

**Q: Can I test workflows locally?**
A: Yes! Use tools like [act](https://github.com/nektos/act) to run GitHub Actions locally.

---

Happy learning! 🎉
