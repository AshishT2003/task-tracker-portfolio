# 🌿 Document 4: Git Workflow & Branching Strategy Rules
> **Project:** Task Management System (Kanban Style)  
> **Version:** 1.0.0  
> **Author:** Ashish Thombare  
> **Date:** 10-Oct-2026  
> **Status:** APPROVED Governance Rule  

---

## 1. Branching Strategy Overview
To maintain maximum codebase stability and enable continuous integration, this project strictly adopts the **Feature Branch Workflow**. Direct code commits to the `main` branch are strictly prohibited during development cycles.

┌───────────────────────────────┐
│   main branch (Stable/Prod)   │
└───────────────┬───────────────┘
│ (Branch Out)
▼
┌─────────────────────────────────────────────────────────────────┐
│ feature/ branches (e.g., feature/task-api, feature/kanban-ui)   │
│ [Isolate Changes] ──► [Test] ──► [Pull Request] ──► [Code Review]│
└────────────────────────────────┬────────────────────────────────┘
│ (Merge Approval)
▼
┌───────────────────────────────┐
│   main branch (Updated/Prod)  │
└───────────────────────────────┘

---

## 2. Core Repository Structure
* **`main` Branch:** This branch represents the production-ready code. It must always compile successfully without errors or broken dependencies. Code enters `main` only via approved Pull Requests (PRs).
* **`feature/` Branches:** Temporary branches created for developing isolated features or fixing bugs (e.g., `feature/task-controller`, `feature/board-ui`). These branches are deleted post-merge.

---

## 3. Step-by-Step Feature Development Protocol
When starting any new task from the project roadmap, developers must strictly adhere to the following sequence:

### Step 3.1: Synchronize with Remote
Always fetch the latest stable code from GitHub before branching out:
```bash
git checkout main
git pull origin main
```

### Step 3.2: Create an Isolated Feature Branch
Name the branch using lowercase letters and descriptive keywords prefixed with `feature/`:
```bash
git checkout -b feature/your-feature-name
```

### Step 3.3: Enforcement of Semantic Commit Messages
Commits must be small, incremental, and follow the **Conventional Commits Specification**:
* `feat:` A new functional feature introduced into the system (e.g., `feat: build task crud endpoints`).
* `fix:` A bug fix introduced into the codebase (e.g., `fix: resolve status validation crash`).
* `docs:` Documentation changes only (e.g., `docs: establish git branching document`).
* `style:` Code formatting, missing semi-colons, white spaces (no architectural change).

### Step 3.4: Pull Request (PR) & Integration
Once development on the feature branch is complete and locally verified:
1. Push the branch to GitHub: `git push origin feature/your-feature-name`
2. Open a **Pull Request (PR)** on GitHub against the `main` branch.
3. Review the code changes, ensure all tests pass, and then merge the PR into `main`.
---