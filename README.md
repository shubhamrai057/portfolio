# portfolio script:
#!/bin/bash

# Configuration
REPO_DIR="$HOME/Documents/projects/portfolio"
BRANCH="main"
GIT_USER="shubhamrai057"
GIT_EMAIL="shubhamrai057@gmail.com"
GIT_REMOTE="origin"
GIT_REMOTE_URL="https://shubhamrai057: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@github.com/shubhamrai057/portfolio.git"

# Debugging
set -x  # Print commands for debugging

# Navigate to repo directory or clone if it doesn't exist
if [ ! -d "$REPO_DIR" ]; then
  git clone "$GIT_REMOTE_URL" "$REPO_DIR"
fi

cd "$REPO_DIR"

# Ensure Git remote is set correctly
git remote set-url origin "$GIT_REMOTE_URL"

# Set Git config (optional)
git config user.name "$GIT_USER"
git config user.email "$GIT_EMAIL"

# Pull latest changes
git checkout $BRANCH
git pull $GIT_REMOTE $BRANCH

# Make changes
echo "Updated on $(date)" >> update-log.txt

# Commit and push
git add .
git commit -m "Automated update on $(date)"
git push $GIT_REMOTE $BRANCH

echo "Changes pushed successfully!"
