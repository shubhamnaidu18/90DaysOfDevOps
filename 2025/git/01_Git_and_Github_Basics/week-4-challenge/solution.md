Week 4: Git and GitHub Challenge
Welcome to the Week 4 Challenge! In this task you will practice the essential Git and GitHub commands and concepts taught by Shubham Bhaiya. This includes:

Git Basics: git init, git add, git commit
Repository Management: git clone, forking a repository, and understanding how a GitHub repo is made
Branching: Creating branches (git branch), switching between branches (git switch / git checkout), and viewing commit history (git log)
Authentication: Pushing and pulling using a Personal Access Token (PAT)
Critical Thinking: Explaining why branching strategies are important in collaborative development
To make this challenge more difficult, additional steps have been added. You will also be required to explore SSH authentication as a bonus task. Complete all the tasks and document every step in solution.md. Finally, share your experience on LinkedIn (details provided at the end).

Challenge Tasks
Task 1: Fork and Clone the Repository
Fork the Repository:

Visit this repository and fork it to your own GitHub account. If not done yet.
Clone Your Fork Locally:

Clone the forked repository using HTTPS:
git clone <your-fork-url>
Change directory into the cloned repository:
cd 2025/git/01_Git_and_Github_Basics
Task 2: Initialize a Local Repository and Create a File
Set Up Your Challenge Directory:

Inside the cloned repository, create a new directory for this challenge:
mkdir week-4-challenge
cd week-4-challenge
Initialize a Git Repository:

Initialize the directory as a new Git repository:
git init
Create a File:

Create a file named info.txt and add some initial content (for example, your name and a brief introduction).
Stage and Commit Your File:

Stage the file:
git add info.txt
Commit the file with a descriptive message:
git commit -m "Initial commit: Add info.txt with introductory content"


Note:
If you follow the above steps exactly, it might not work as expected. When you create a new folder and run git init inside it, you're actually creating a new Git repository inside the main repository. This causes the folder (in this case, week-4-challenge) to be treated as a Git submodule, which can lead to issues when you try to push your changes. You may not be able to push the folder and its files to the remote repository.

Solution:
Instead of initializing a new Git repo inside the challenge folder, follow these steps:

First, go to the root of your main repository (for example, 90DaysOfDevOps).

Run git pull origin master to make sure your local copy is up to date with the remote repo.

Then navigate to the appropriate directory (like 2025/git/01_Git_and_Github_Basics) and create your week-4-challenge folder inside it.

Add your files (e.g., info.txt), stage them using git add, commit them with git commit, and finally push using:


git push origin master
This will ensure your changes are correctly pushed to the remote GitHub repository without any submodule issue



Task 3: Configure Remote URL with PAT and Push/Pull
Configure Remote URL with Your PAT:
To avoid entering your Personal Access Token (PAT) every time you push or pull, update your remote URL to include your credentials.

⚠️ Note: Embedding your PAT in the URL is only for this exercise. It is not recommended for production use.

Replace <your-username>, <your-PAT>, and <repository-name> with your actual GitHub username, your PAT, and the repository name respectively:

git remote add origin https://<your-username>:<your-PAT>@github.com/<your-username>/90DaysOfDevOps.git
If a remote named origin already exists, update it with:

git remote set-url origin https://<your-username>:<your-PAT>@github.com/<your-username>/90DaysOfDevOps.git
Push Your Commit to Remote:

Push your current branch (typically main) and set the upstream:
git push -u origin main
(Optional) Pull Remote Changes:

Verify your configuration by pulling changes:
git pull origin main


Note: For the above task, I followed these steps:

Added the remote origin using the HTTPS URL of my 90DaysOfDevOps repository:


git remote add origin <your-repo-url>
Then I updated the remote URL (if already set) using:

git remote set-url origin <your-repo-url>
These steps should be done from the root (main) folder of your repository — i.e., 90DaysOfDevOps.

Once that’s done, navigate to the week-4-challenge folder, make your changes, and push them using:

git push origin master
   



Task 4: Explore Your Commit History

View the Git Log:
Check your commit history using: git log
Take note of the commit hash and details as you will reference these in your documentation.

Task 5: Advanced Branching and Switching
Create a New Branch:

Create a branch called feature-update:
git branch feature-update
Switch to the New Branch:

Switch using git switch:
git switch feature-update
Alternatively, you can use:
git checkout feature-update
Modify the File and Commit Changes:

Edit info.txt (for example, add more details or improvements).
Stage and commit your changes:
git add info.txt
git commit -m "Feature update: Enhance info.txt with additional details"
git push origin feature-update
Merge this branch to main via a Pull Request on GitHub.
(Advanced) Optional Extra Challenge:

If you feel confident, create another branch (e.g., experimental) from your main branch, make a conflicting change to info.txt, then switch back to feature-update and merge experimental to simulate a merge conflict. Resolve the conflict manually, then commit the resolution.
Note: This extra step is optional and intended for those looking for an additional challenge.

Task 6: Explain Branching Strategies
Document Your Process:
Create (or update) a file named solution.md in your repository.
List all the Git commands you used in Tasks 1–4.
Explain: Write a brief explanation on why branching strategies are important in collaborative development. Consider addressing:
Isolating features and bug fixes
Facilitating parallel development
Reducing merge conflicts
Enabling effective code reviews

🧠 Why Branching Strategies Are Important in Collaborative Development
When multiple people are working on the same codebase, things can get messy really fast. That's where branching strategies come in—they help keep everything clean, organized, and under control.

Here’s why they’re so important:

🧩 1. Isolating Features and Bug Fixes
Instead of working directly on the main code, developers create separate branches for new features or bug fixes. This way:

You can work without affecting the main project.

If something breaks, it doesn’t impact everyone else.

It’s easy to test and review just that piece of work.

👥 2. Facilitating Parallel Development
Branching lets different people (or teams) work on different tasks at the same time without stepping on each other’s toes. For example:

One person can be building a login system.

Another can be fixing a design bug.

Both can work independently and merge their work later.

🔀 3. Reducing Merge Conflicts
When changes are isolated in separate branches, it's easier to merge them safely. You get fewer situations where two people edited the same file at the same time—aka merge conflicts, which are annoying and tricky to fix.

👀 4. Enabling Effective Code Reviews
Before merging a branch into the main project, teams often review the code through Pull Requests (PRs). This helps:

Catch bugs or mistakes.

Share knowledge across the team.

Ensure code meets the team's quality standards.







Bonus Task: Explore SSH Authentication
Generate an SSH Key (if not already set up):

Create an SSH key pair:
ssh-keygen
Follow the prompts and then locate your public key (typically found at ~/.ssh/id_ed25519.pub).
Add Your SSH Public Key to GitHub:

Copy the contents of your public key and add it to your GitHub account under SSH and GPG keys.
(See Connecting to GitHub with SSH for help.)
Switch Your Remote URL to SSH:

Change the remote URL from HTTPS to SSH:
git remote set-url origin git@github.com:<your-username>/90DaysOfDevOps.git
Push Your Branch Using SSH:

Test the SSH connection by pushing your branch:
git push origin feature-update
📢 How to Submit
Push Your Final Work:

Ensure your branch (e.g., feature-update) with the updated solution.md file is pushed to your fork.
Create a Pull Request (PR):

Open a PR from your branch to the main repository.
Use a clear title such as:
Week 4 Challenge - DevOps Batch 9: Git & GitHub Advanced Challenge
In the PR description, summarize your process and list the Git commands you used.
