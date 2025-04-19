Week 4: Git & GitHub Advanced Challenge
This challenge covers advanced Git concepts essential for real-world DevOps workflows. By the end of this challenge, you will:
•	Understand how to work with Pull Requests effectively.
•	Learn to undo changes using Reset & Revert.
•	Use Stashing to manage uncommitted work.
•	Apply Cherry-picking for selective commits.
•	Keep a clean commit history using Rebasing.
•	Learn industry-standard Branching Strategies.
Topics Covered
1.	Pull Requests – Collaborating in teams.
2.	Reset & Revert – Undo changes safely.
3.	Stashing – Saving work temporarily.
4.	Cherry-picking – Selecting specific commits.
5.	Rebasing – Maintaining a clean history.
6.	Branching Strategies – Industry best practices.
Challenge Tasks
Task 1: Working with Pull Requests (PRs)
Scenario: You are working on a new feature and need to merge your changes into the main branch using a Pull Request.
1.	Fork a repository and clone it locally.
2.	git clone <your-forked-repo-url>
cd <repo-name>
3.	Create a feature branch and make changes.
4.	git checkout -b feature-branch
5.	echo "New Feature" >> feature.txt
6.	git add .
git commit -m "Added a new feature"
![image](https://github.com/user-attachments/assets/8109a314-b053-470a-8129-460641315a77)

 

7.	Push the changes and create a Pull Request.
git push origin feature-branch
8.	Open a PR on GitHub, request a review, and merge it once approved.

Steps :-
•	Open your GitHub profile.
•	Navigate to the repository and lick “Compare & Pull Request”

![image](https://github.com/user-attachments/assets/ef2cd693-e5a2-4972-ac27-b603d8be0fff)

 
•	Select the base branch where you want to merge and select from which branch you want to merge.
•	Then create pull request.
 ![image](https://github.com/user-attachments/assets/3cead55f-8102-4ee8-85b1-95727e4382a6)
 
•	Once click on the Create pull request.
![image](https://github.com/user-attachments/assets/1fc0a5e8-b3ae-4ff2-9e32-dc21d06bac45)
 
•	You need to add the Description also you can ask your senior or colleague to review the pull request and the file that you have created.
•	Once you have assigned the reviewers and the description, then you can create pull request.
 ![image](https://github.com/user-attachments/assets/f7a892bb-f511-453c-b605-07904284cac4)

•	As you can see in the screenshot there is no reviewers in it but assume you have assigned the reviewer and they have reviewed the request and approved it.
•	Once it is approved you can see the latest comment.
•	If it is mentioned that it is approved then you just need to click on merge pull request.
•	Then it will ask you to confirm the merge before that always put description.
 ![image](https://github.com/user-attachments/assets/205e931f-bf12-4c75-9964-e99fa31c3a91)

•	Once you click on confirm merge then pull request will be succeed.
  ![image](https://github.com/user-attachments/assets/dff7fdd0-0282-4a5a-8f65-82d25eddd467)


Document in solution.md
•	Steps to create a PR.
•	Best practices for writing PR descriptions.
•	Handling review comments.
🛠️ Pull Request (PR) Workflow Guide
✅ Steps to Create a Pull Request (PR)
1.	Create a Feature Branch

git checkout -b feature/your-feature-name
2.	Make Changes and Commit
git add .
git commit -m "Add a meaningful commit message"
3.	Push the Feature Branch
git push origin feature/your-feature-name
4.	Open a Pull Request on GitHub
o	Navigate to the repository.
o	Click "Compare & Pull Request".
o	Choose the base branch (e.g., main or develop) and your feature branch.
o	Add a title and description, then click "Create Pull Request".
________________________________________
✍️ Best Practices for Writing PR Descriptions
Clear communication in PRs improves collaboration and code quality.
Structure your description like this:
🔍 What does this PR do?
Brief summary of the change.
E.g., "Implements login functionality using JWT."
📋 Changes made
•	Added authService.ts for token generation.
•	Updated login API to validate credentials.
•	Added unit tests.
✅ Checklist
•	Code is linted
•	Unit tests added
•	No breaking changes
📝 Related Issue
Closes #123 or Fixes bug described in [link]
________________________________________
💬 Handling Review Comments
1.	Stay open to feedback
Reviews are about the code, not you.
2.	Reply to each comment
Acknowledge the feedback. Use:
o	✅ Fixed
o	🤔 Need clarification
o	🚫 Won’t fix (with reason)
3.	Make necessary changes
Update your branch with changes and push again:
git add .
git commit -m "Refactor: address review feedback"
git push origin feature/your-feature-name
4.	Resolve comments on GitHub
Mark them as "Resolved" once handled.

Task 2: Undoing Changes – Reset & Revert
Scenario: You accidentally committed incorrect changes and need to undo them.
1.	Create and modify a file.
2.	echo "Wrong code" >> wrong.txt
3.	git add .
 ![image](https://github.com/user-attachments/assets/a9c154fd-1ae3-4a18-bdaf-745b77da128f)

git commit -m "Committed by mistake"

4.	Soft Reset (keeps changes staged).
git reset --soft HEAD~1:- it will untrack and stag the file last committed file.
![image](https://github.com/user-attachments/assets/9c77fc7a-a136-4e04-9c04-aa3dd4d7d432)

 
5.	Mixed Reset (unstages changes but keeps files).
git reset --mixed HEAD~1 :- it will untrack the file last committed file.
 ![image](https://github.com/user-attachments/assets/f66e437b-2421-41e9-add0-64fe9aaba94a)

6.	Hard Reset (removes all changes).
git reset --hard HEAD~1 :- it will delete the file last committed file.
 ![image](https://github.com/user-attachments/assets/e290ca83-61e6-4179-ae4b-8940be08fb51)

As you can see wrong file is deleted and it also not in untrack.

7.	Revert a commit safely.
git revert HEAD :- it will revert the last head commit.
As per last command git reset –hard it will delete the committed the file(wrong file) and the log for it.
Not when you do revert HEAD then it will revert the last committed file that will feature file which was committed in task 1.

Document in solution.md
•	Differences between reset and revert.
•	When to use each method.

🔁 Differences Between git reset and git revert
🧠 Conceptual Difference
Feature	git reset	git revert
What it does	Moves the branch pointer to an earlier commit	Creates a new commit that undoes a previous one
Affects history	Rewrites commit history	Preserves history
Safe for shared branches	❌ No (can cause issues for others)	✅ Yes (safe for collaboration)
Undo visibility	Changes are not visible to others (unless pushed with --force)	Revert is visible as a new commit
________________________________________
🧪 When to Use Each Method
✅ Use git reset when:
•	You're working locally, and
•	You want to undo commits or unstage files without keeping the history.
•	Useful during development or practice.
Example:
bash
CopyEdit
git reset --soft HEAD~1  # Undo commit but keep changes staged
git reset --mixed HEAD~1 # Undo commit and unstage changes
git reset --hard HEAD~1  # Undo commit and discard changes (use with caution!)
✅ Use git revert when:
•	You're working on a shared branch (e.g., main, develop)
•	You want to safely undo a specific commit while keeping the history.
•	You need traceability and accountability for changes.
Example:
bash
CopyEdit
git revert <commit-hash>  # Creates a new commit that undoes the target
________________________________________
💡 Tip:
Use reset during local development.
Use revert when collaborating with others.






