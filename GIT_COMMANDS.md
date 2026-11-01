Here are some of the basic Git commands you might use on the command line when working with GitHub:

### 1. **Setting Up Git**
   - **`git config --global user.name "Your Name"`**: Sets your GitHub username.
   - **`git config --global user.email "your_email@example.com"`**: Sets your GitHub email.

### 2. **Creating a New Repository**
   - **`git init`**: Initializes a new Git repository in the current directory.

### 3. **Cloning a Repository**
   - **`git clone <repository_url>`**: Copies an existing GitHub repository to your local machine.

### 4. **Checking Repository Status**
   - **`git status`**: Shows the status of your files in the working directory and staging area.

### 5. **Staging and Committing Changes**
   - **`git add <file>`**: Stages a specific file for commit.
   - **`git add .`**: Stages all changes in the current directory (including subdirectories).
   - **`git commit -m "Commit message"`**: Commits the staged changes with a message.

### 6. **Branching**
   - **`git branch`**: Lists all branches in your repository.
   - **`git branch <branch_name>`**: Creates a new branch.
   - **`git checkout <branch_name>`**: Switches to the specified branch.
   - **`git checkout -b <branch_name>`**: Creates and switches to a new branch.

### 7. **Merging Branches**
   - **`git merge <branch_name>`**: Merges the specified branch into the current branch.

### 8. **Viewing Commit History**
   - **`git log`**: Shows a list of all commits in the current branch.
   - **`git log --oneline`**: Shows a condensed version of the commit history.

### 9. **Pushing Changes**
   - **`git push origin <branch_name>`**: Pushes the committed changes to a remote repository on the specified branch.

### 10. **Pulling Changes**
   - **`git pull`**: Fetches and merges changes from the remote repository into the current branch.

### 11. **Discarding Changes**
   - **`git checkout -- <file>`**: Discards changes in a specific file.
   - **`git reset --hard HEAD`**: Discards all changes and resets the working directory to the last commit.

### 12. **Deleting Branches**
   - **`git branch -d <branch_name>`**: Deletes the specified branch locally.
   - **`git push origin --delete <branch_name>`**: Deletes the specified branch from the remote repository.

### 13. **Tagging**
   - **`git tag -a v1.0 -m "Version 1.0"`**: Creates a new tag for a specific commit with a message.
   - **`git push origin --tags`**: Pushes all tags to the remote repository.

These commands will help you manage your projects using Git from the command line efficiently.