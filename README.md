# Lab M5.03 - GitOps Workflow Implementation

**Cloud Engineering Bootcamp - Week 5, Day 2**  
**Module:** Cloud Automation & CI/CD

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

## 🚀 Submission

Submit your repository URL through the course platform.
