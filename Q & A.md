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
**Fork**                 
Creates an independent copy of someone else's repository on my GitHub account.**   
**Clone**                   
Downloads an existing repository to my local machine.**

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
**GitFlow is a structured Git branching strategy that uses main, develop, feature, release, and hotfix branches.**     
**Developers work on separate feature branches, merge completed features into develop, prepare releases using release branches, and use hotfix branches to fix critical production issues.**      
**It helps maintain stable production code and organized release management.**   

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

### 18. When do merge conflicts occur?

### 19. How do you resolve merge conflicts?

### 20. What happens if two developers modify the same file?

### 21. How do you avoid merge conflicts?
 **I avoid merge conflicts by frequently pulling the latest changes, keeping feature branches short-lived, communicating with team members, making small commits, and regularly merging changes from the main branch into my feature branch.**

### 22. How do you see conflicting files?
**We use `git status` to identify conflicting files during a merge conflict.** 

### 23. What is git stash?
**Git stash temporarily saves uncommitted changes without creating a commit, allowing you to switch branches or work on something else and restore those changes later.**   
```
git stash          # Save changes
git stash list     # View saved stashes
git stash pop      # Restore and remove latest stash
git stash apply    # Restore but keep stash
```

### 24. What is git reset?
**Git reset is used to undo commits by moving the HEAD pointer to a previous commit.**   
**It has three modes:**   
- `--soft` (keeps changes staged),   
- `--mixed` (keeps changes unstaged),    
- `--hard` (discards changes).

### 25. What is git revert?
**Git revert is used to undo a specific commit by creating a new commit that reverses its changes without rewriting the existing Git history.**   
`git revert <commit-id>` 

### 26. What are Git tags?
**Git tags are used to mark specific commits, usually for software releases or version numbers like `v1.0` `v2.0`, making it easier to identify and track release versions.**

### 27. What is git rebase?
**Git rebase is used to move or replay commits from one branch onto another branch, creating a cleaner, linear commit history.**   
```
git checkout feature
git rebase main
```

### 28. Difference between merge and rebase?
- **Git Merge combines changes from two branches and creates a merge commit (when needed), preserving branch history.**   
- **Git Rebase moves commits onto another branch to create a cleaner, linear history.**  

### 29. When should you use rebase?
**Use Git rebase when you want to update your feature branch with the latest changes from the main branch and maintain a clean, linear commit history, preferably before merging your feature branch. Avoid rebasing shared branches.**

### 30. What Git workflow do you use in your team?
- **We follow a feature-based Git workflow similar to GitHub Flow.**   
- **Developers create feature branches, commit and push changes, raise Pull Request, and undergo code reviews.**   
- **Jenkins runs automated CI/CD check, and after approval, changes are merger into the main branch and deployed.** 

### 31. How do developers collaborate using Git?
### 32. How do you manage multiple developers working on same repo?
### 33. How do you protect main branch?
### 34. What is a pull request?
### 35. What is a code review?
### 36. What is a merge request?
### 37. What happens when a wrong commit is pushed to production branch?
### 38. How do you rollback a bad deployment using Git?
### 39. How do you handle large repositories?
### 40. How do you manage Git access control?
### 41. How do you integrate Git with CI/CD?
### 42. How does Jenkins trigger pipeline using Git?
### 43. How do you store infrastructure code in Git?
### 44. How do you manage multiple environments with Git branches?
### 45. What is GitOps?
### 46. How do you fix accidentally committed secrets?
### 47. How do you prevent secrets in Git?
### 48. What is Git secret scanning?
### 49. How do you manage SSH keys for Git access?
