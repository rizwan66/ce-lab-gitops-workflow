# Lab M5.03 - GitOps Workflow Implementation

**Cloud Engineering Bootcamp - Week 5, Day 2**  
**Module:** Cloud Automation & CI/CD

## Start Here: Fork, Clone, and Submit

You will complete this lab by working in **your own fork** of the lab repository and submitting a **Pull Request (PR)**.
1. **Fork the lab repository** to your GitHub account.
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/<your-github-username>/ce-lab-gitops-workflow.git
   cd ce-lab-gitops-workflow
   ```

3. **Follow all instructions below** and save your work in this repo (files, screenshots, and notes).
4. **When finished, submit your work:**
   - `git add` → `git commit` → `git push`
   - Open a **Pull Request** from your fork back to the original lab repo
   - Copy the **PR URL** and paste it into the **Lab Submission** field in the Student Portal

## 📋 Lab Overview

Implement a complete GitOps workflow where infrastructure changes are managed entirely through Git. Learn declarative infrastructure management and automated synchronization.

## 🎯 Learning Objectives

- Implement GitOps principles and workflows
- Configure automated drift detection
- Set up pull request-based infrastructure updates
- Implement automated reconciliation
- Use Git as single source of truth

## 📁 Repository Structure

```
ce-lab-gitops-workflow/
├── .github/
│   └── workflows/
│       ├── drift-detection.yml
│       ├── pr-plan.yml
│       └── sync.yml
├── infrastructure/
│   ├── dev/
│   ├── staging/
│   └── prod/
├── README.md
└── .gitignore
```

## ✅ Submission Requirements

Complete the lab as described in the instructions and save your work in this repo (files, screenshots, and notes):

1. **GitOps Workflows**
   - Drift detection workflow
   - PR-based plan workflow
   - Automated sync on merge

2. **Multi-environment Setup**
   - Dev, staging, and prod environments
   - Environment-specific configurations

3. **Documentation**
   - GitOps workflow explanation
   - Drift handling procedures

**Reminder:** After pushing your work and opening a PR:
- Copy the **PR URL**
- Paste it into the **Lab Submission** field in the Student Portal

## 🎓 Grading Rubric

| Criteria | Points |
|----------|--------|
| **GitOps Implementation** | 35 |
| **Drift Detection** | 25 |
| **Multi-environment Setup** | 25 |
| **Documentation** | 15 |
| **Total** | 100 |

## 💡 Tips

- Use scheduled workflows for drift detection
- Implement PR comments for plan output
- Use environment protection rules
- Test drift detection by making manual changes

## 📚 Resources

- [GitOps Principles](https://opengitops.dev/)
- [GitHub Environments](https://docs.github.com/en/actions/deployment/targeting-different-environments)

<!-- ## 🚀 Submission

Submit your repository URL through the course platform. -->

---

## Lab M5.03 - Implementation

### GitOps Flow

```
develop branch ──push──► Deploy to dev environment
    │
    └──PR──► Promotion Check (plan against prod)
                │
                └──merge──► main branch ──push──► Deploy to prod environment
```

### Environments

| Environment | Branch | Versioning | Log Retention | State Key |
|-------------|--------|------------|---------------|-----------|
| dev | develop | Disabled | 7-14 days | m5-03-gitops/dev/terraform.tfstate |
| prod | main | Enabled | 90 days | m5-03-gitops/prod/terraform.tfstate |

### Workflows

| Workflow | Trigger | Purpose |
|----------|---------|---------|
| `deploy.yml` | Push to main or develop | Deploy to the matching environment |
| `promotion.yml` | PR targeting main | Plan prod changes and post to PR |
| `drift-detection.yml` | Nightly at 02:00 UTC / manual | Detect out-of-band infrastructure changes |

### How to Promote Changes
1. Make changes on `develop` and push
2. Verify the dev deployment succeeds
3. Open a PR from `develop` to `main`
4. Review the production plan in the PR comment
5. Merge to deploy to production

### Drift Detection
The nightly drift detection job runs `terraform plan -detailed-exitcode` against both environments.
If exit code `2` is returned (changes detected), a GitHub Issue is automatically opened with the plan diff,
alerting the team that infrastructure was modified outside of Terraform.
