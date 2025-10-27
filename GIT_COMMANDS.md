# Git Commands for ResuMate

## Standard Workflow to Push Changes

### 1. Check what files have changed
```bash
git status
```

### 2. Add changed files to staging
```bash
# Add specific file
git add filename.js

# Add all changes
git add .

# Add all changes in specific directory
git add backend/
```

### 3. Commit changes with a message
```bash
git commit -m "Your commit message describing the changes"
```

### 4. Push to GitHub
```bash
git push
```

## Complete Example
```bash
# Check status
git status

# Add all changes
git add .

# Commit with message
git commit -m "Fixed button colors and added API integration"

# Push to GitHub
git push
```

## Advanced Commands

### Pull latest changes from GitHub
```bash
git pull
```

### Check commit history
```bash
git log
```

### Undo last commit (keep changes)
```bash
git reset --soft HEAD~1
```

### Undo last commit (discard changes)
```bash
git reset --hard HEAD~1
```

### Create and switch to new branch
```bash
git checkout -b feature-name
```

### Push new branch to GitHub
```bash
git push -u origin branch-name
```

### View differences
```bash
git diff
git diff filename.js
```

## Troubleshooting

### If push is rejected
```bash
git pull origin main
# Resolve conflicts if any
git push
```

### Force push (use with caution!)
```bash
git push --force
```

## Current Remote Repository
Your repository is configured to push to:
```
https://github.com/coderanant1/ResuMate.git
```

