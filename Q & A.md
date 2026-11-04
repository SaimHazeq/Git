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
**Fork creates an independent copy of someone else's repository on my GitHub account, Whereas Clone downloads an existing repository to my local machine.**

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
### 10. How do you stage specific files?
### 11. What is Git branching strategy?
### 12. What is GitFlow?
### 13. What is trunk-based development?
### 14. How do you manage multiple environments (dev, staging, prod) using Git?
### 15. How do you ensure code stability in production branch?
### 16. How do you manage hotfix deployment?
### 17. What is a merge conflict?
### 18. When do merge conflicts occur?
### 19. How do you resolve merge conflicts?
### 20. What happens if two developers modify the same file?
### 21. How do you avoid merge conflicts?
### 22. How do you see conflicting files?
### 23. What is git stash?
### 24. What is git reset?
### 25. What is git revert?
### 26. What are Git tags?
### 27. What is git rebase?
### 28. Difference between merge and rebase?
### 29. When should you use rebase?
### 30. What Git workflow do you use in your team?
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
