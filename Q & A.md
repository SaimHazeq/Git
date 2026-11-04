### 1. What is Git?
**Git is distributed version control system used to track changes in source code during software development. It allows multiple developers to collaborate, maintain version history, create branches, and revert changes when necessary**

### 2. What is the HEAD in Git?
**HEAD is a pointer to the current commit or the currently checked-out branch.**  
`Example: HEAD -> main -> commit123 `   
**When switching branches, HEAD moves to that branch.**


### 3. What is the difference between Git clone and Git pull?
**git clone**    
- Copies an entire repository  
- Used first time                                           
`git clone repo_url`

**git pull**  
- Fetches latest changes from remote  
- updates existing repo                                                  
`git pull origin main`   

### 4. What is the difference between Git fetch and Git pull?
**git fetch**  
- Downloads changes
- Does NOT merge  
 
**git pull**
- Fetch + merge                                          
`git fetch origin`                                                               
`git merge origin/main`  

### 5. What is the difference between Git merge and Git rebase?  
**git merge**  
- merge combines changes from one into another.                    
`git checkout main`                     
`git merge feature-login`                                          
- Git creates a merge commit.        

**git rebase**
- rebase mover or reapplies commits from one branch onto another branch.        
- Instead of merge commits, it creates a linear history.                       
`git checkout feature`                           
`git rebase main`  

### 6. What is the difference between fork and clone?   
**fork**                 
- Creates an independent copy of someone else's repository on my GitHub account.

**clone**                   
- Downloads an existing repository to my local machine.

### 7. How do you rollback changes?
- **If I need to rollback changes in Git, I first identify the stage of the changes.**  
- **If the changes are not committed, I use `git restore`. If they are committed but not pushed, I can use `git reset` depending on whether I want to keep or discard the changes.**   
- **If changes are already pushed to a shared repository, I prefer `git revert` because it creates a new commit that reverses the previous changes without rewriting Git history.**  
- **For production deployments, I would identify the last stable application version and rollback using the deployment tool. For Kubernetes, I use `kubectl rollout undo`, and then verify pod health, application logs and service availability.**

### 8. How do you reset a commit?
**We use `git reset` to undo a commit.**            
Example: `git reset --soft HEAD~1`                           
**Removes the last commit while keeping the changes staged.**

### 9. How do you revert a commit?
**We use `git revert <commit-id>` to undo a specific commit by creating a new commit that reverses its changes without rewriting Git history.**

### 10. How do you stage specific files?
**We use `git add <filename>` to stage a specific file.**

### 11. What is Git branching strategy?
**A Git branching strategy is a workflow for creating and managing branches so multiple developers can work on features, bug fixes, and releases without affecting the main production code.**

### 12. What is GitFlow?
- **GitFlow is a structured Git branching strategy that uses main, develop, feature, release, and hotfix branches.**     
- **Developers work on separate feature branches, merge completed features into develop, prepare releases using release branches, and use hotfix branches to fix critical production issues.**      
- **It helps maintain stable production code and organized release management.**   

### 13. What is trunk-based development?
- **Trunk-Based Development is a Git branching strategy where developers frequently integrate small code changes into a single main branch.**   
- **It uses short-lived feature branches or direct commits, along with automated testing and CI/CD pipelines.**   
- **This reduce merge conflicts, improves collaboration, and supports faster software delivery.**  

### 14. How do you manage multiple environments (dev, staging, prod) using Git?
**We manage multiple environments using separate branches, environment-specific configuration files, and CI/CD pipelines to ensure code is properly tested before reaching production.**    
```
main                               
 |                                 
develop                             
 |                                   
feature/login                          
 |                           
Dev → Staging → Production                          
```

- Develop: For development and testing
- Staging: For pre-production validation.
- Main: For production-ready code.

**We maintain separate configuration files:**   
```
config/
  dev.yaml
  staging.yaml
  prod.yaml
  ```
**Each environments has its own configuration, credentials, and resource settings.**                  
**Secrets should be stored in secrets manages, not committed to Git.**  

### 15. How do you ensure code stability in production branch?
- **I ensure production stability by implementing branch protection rules, mandatory Pull Request reviews, automated testing, Jenkins CI/CD validation, code quality checks using SonarQube, and security scanning using Trivy.**   
- **I also restrict direct pushes to the main branch and allow merging only after successful testing and approval.**  

### 16. How do you manage hotfix deployment?
- **I create a hotfix branch from the production `(main)` branch, fix the critical issue, test the changes, and raise a Pull Request for approval.**   
- **After approval, I merge it into main and deploy through the CI/CD pipeline.**  
- **Finally, I merge the hotfix back into the develop branch to keep both branches synchronized.**  

### 17. What is a merge conflict?
- **A merge conflict occurs when Git cannot automatically merge changes because two branches have modified the same lines of a file differently.**   
- **Example: Two developers modify the same line in a file. Git cannot decide which change to keep, so we must resolve the conflict manually, test the changes, and complete the merge.**  

### 18. How do you avoid merge conflicts?
 **I avoid merge conflicts by frequently pulling the latest changes, keeping feature branches short-lived, communicating with team members, making small commits, and regularly merging changes from the main branch into my feature branch.**

### 19. How do you see conflicting files?
**We use `git status` to identify conflicting files during a merge conflict.** 

### 20. What is git stash?
**git stash temporarily saves uncommitted changes without creating a commit, allowing you to switch branches or work on something else and restore those changes later.**   
```
git stash          # Save changes
git stash list     # View saved stashes
git stash pop      # Restore and remove latest stash
git stash apply    # Restore but keep stash
```

### 21. What is git reset?
**git reset is used to undo commits by moving the HEAD pointer to a previous commit.**   
**It has three modes:**   
- `--soft` (keeps changes staged),   
- `--mixed` (keeps changes unstaged),    
- `--hard` (discards changes).

### 22. What is git revert?
**git revert is used to undo a specific commit by creating a new commit that reverses its changes without rewriting the existing Git history.**   
`git revert <commit-id>` 

### 23. What are Git tags?
**git tags are used to mark specific commits, usually for software releases or version numbers like `v1.0` `v2.0`, making it easier to identify and track release versions.**

### 24. What is git rebase?
**git rebase is used to move or replay commits from one branch onto another branch, creating a cleaner, linear commit history.**   
```
git checkout feature
git rebase main
```

### 25. Difference between merge and rebase?
**git merge**   
- combines changes from two branches and creates a merge commit (when needed), preserving branch history.
               
**git rebase**   
- moves commits onto another branch to create a cleaner, linear history.  

### 26. When should you use rebase?
**Use Git rebase when you want to update your feature branch with the latest changes from the main branch and maintain a clean, linear commit history, preferably before merging your feature branch. Avoid rebasing shared branches.**

### 27. What Git workflow do you use in your team?
- **We follow a feature-based Git workflow similar to GitHub Flow.**   
- **Developers create feature branches, commit and push changes, raise Pull Request, and undergo code reviews.**   
- **Jenkins runs automated CI/CD check, and after approval, changes are merger into the main branch and deployed.** 

### 28. How do developers collaborate using Git?
**Developers collaborate using Git by working on separate feature branches, committing and pushing changes to a shared remote repository, creating Pull Request, reviewing each other's code, resolving merge conflicts, and merging approved changes into the main branch.**

### 29. How do you manage multiple developers working on same repo?
**I manage multiple developers by assigning separate feature branches, following a common branching strategy, encouraging frequent commits and pulls, enforcing Pull Request reviews, resolving merge conflicts, and protecting the main branch to maintain code quality and stability.**

### 30. How do you protect main branch?
**I protect the main branch by enabling branch protection rule, restricting direct pushes, requiring Pull Request approvals, enforcing automated CI/CD checks, and allowing only authorized developers to merge code.**

### 31. What is a pull request?
**A Pull Request(PR) is a request to merge code changes from one branch into another, allowing team members to review, discuss, and approve the changes before merging.**

### 32. What is a code review?
**Code review is the process of examining another developer's code to identify bugs, security issues, coding mistakes, and quality improvements before merging it into the main branch.**

### 33. What is a merge request?
**A Merge Request(MR) is a request to merge code changes from one branch into another after code review and approval. It is Gitlab's equivalent of a Pull Request(PR) in GitHUb/**

### 34. What happens when a wrong commit is pushed to production branch?
**When a wrong commit is pushed to the production branch, it can introduce bugs, break application functionality, cause service downtime, or affect users until the issue is fixed or rolled back.**

### 35. How do you rollback a bad deployment using Git?
**I identify the fault commit, use `git revert <commit-id>` to reverse the changes, push the new commit, and trigger the CI/CD pipeline to redeploy the last stable application version.**

### 36. How do you handle large repositories?
**I manage large repositories by using Git LFS for large files, shallow clones to reduce download time, sparse checkout to work with specific directories, and proper branching strategies to maintain performance and organization.**

### 37. How do you manage Git access control?
**I manage Git access control using role-based permissions, SSH authentication, branch protection rules, least-privilege access, and mandatory Pull Request approvals to ensure only authorized developers can modify or merge code.**

### 38. How do you integrate Git with CI/CD?
**I integrate Git with CI/CD using webhooks. Whenever a developer pushes code or creates a Pull Request, Jenkins automatically triggers the pipeline to perform code checkout, build, testing, security scanning, and deployment.**

### 39. How does Jenkins trigger pipeline using Git?
**Jenkins triggers a pipeline using Git Webhooks. Whenever a developer pushed code to GitHub, a webhook sends a notification to Jenkins, which automatically starts the configured CI/CD pipeline.**

### 40. How do you store infrastructure code in Git?
**I store infrastructure code such as Terraform and Ansible playbooks in a Git Repository, organize it into modules and environment-specific directories, and use feature branches, Pull Requests, and code reviews to manage changes safely.**

### 41. How do you manage multiple environments with Git branches?
**I use separate branches such as `develop`, `staging` and `main` for Dev, Staging and Production, respectively. Changes are tested in Dev, promoted to Staging, and merged into Production after successful testing and approval.**

### 42. What is GitOps?
**GitOps is a DevOps practice where Git acts as the Single source of truth for infrastructure and application configurations. Tools like ArgoCD or Flux continuously monitor the Git repository and automatically synchronize with the Kubernetes Cluster.**

### 43. How do you fix accidentally committed secrets?
**I immediately revoke and rotate the exposed credentials, remove the secrets from the repository, clean Git history if necessary, and use a secret manager like AWS Secret Manager to store credentials securely.**

### 44. How do you prevent secrets in Git?
**I prevent secrets in Git by using AWS Secret Manager or environment variables, adding sensitive files to `.gitignore`, enabling pre-commit secret scannign, and never hardcoding credentials in source code.**

### 45. What is Git secret scanning?
**Git secret scanning is a security process that detects sensitive information like passwords, API keys, and access tokens in Git repositories before they are committed or pushed.**

### 46. How do you manage SSH keys for Git access?
**I generate SSH key pairs, add the public key to GitHub, securely store the private key, configure SSH authentication, and regularly rotate keys while revoking unused keys.**
