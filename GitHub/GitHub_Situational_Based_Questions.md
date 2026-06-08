# Cherry Pick Scenarios
## Q : 
- You have a branch with 10 Commits. 
- Only commit #5 contains a bug fix needed urgently in production. 
- How will you move only that fix to the release branch?  
Ans: 
-- I would use git cherry-pick. First I'd identify the hash of the bug-fix commit, switch to the release branch, and run git cherry-pick <commit-hash>. This brings only that specific fix into the release branch without merging the other unfinished commits.
-- Command : 
    git checkout release-branch
    git cherry-pick <commit-hash-of-commit-5>


## Q : 
- You cherry-picked a commit but got merge conflicts. 
- What steps would you follow?
Ans :
-- Approach
    - Run git status to see conflicted files.
    - Open the files and resolve the conflicts manually.
    - Stage the resolved files: **git add.**
    - Continue the cherry-pick: **git cherry-pick --continue**
-- If you don't want to proceed: **git cherry-pick --abort**


## Q : 
- You accidentally cherry-picked the wrong commit. 
- How will you undo it?
Ans : 
-- If not Pushed Yet : **git reset --hard HEAD~1**
-- If already pushed/shared: **git revert <cherry-pick-commit-hash>** 


## Q : 
- After cherry-picking, Git created a new commit hash. 
- Why?
Ans : Cherry-pick doesn't move the original commit; it creates a new commit with the same changes on another branch. Since the parent commit and metadata are different, Git generates a new commit hash.


# Merge vs Rebase Scenarios
## Q : 
- You are working on Feature Branch. 
- Main branch received 50 new commits.
Ans : 
-- Rebase : If the team prefers a clean linear history, I'd use rebase
    git checkout feature-branch
    git fetch
    git rebase main
-- Merge : If preserving branch history is important, I'd use merge.
    git checkout feature-branch
    git merge main

## Q :
- You already pushed your branch.
- Now you perform rebase.
- What problem can occur?
Ans : 
-- Rebase rewrites commit history and creates new commit hashes.
-- If the branch was already pushed, your local history will no longer match the remote branch, and a normal push will fail.
-- You may need : **git push --force**
-- This can overwrite history and affect teammates working on the same branch.

## Q : 
- Your team prefers clean history.
- Would you choose merge or rebase?
- Explain.
Ans : For Clean History Prefer "Rebase"

## Q : 
- You rebased a branch and lost some commits.
- How would you recover them?
- (Hint: Reflog)
Ans :
-- Use Reflog to find the previous state of the branch: 
    **git reflog**
-- Find the commit before the rebase and reset backk to it :
    **git reset --hard <commit-hash>**

# Pull Request Scenarios
## Q :
- Your PR contains 25 commits.
- Reviewer asks: "Can you squash them into a single commit?"
- How Will You Do it?
Ans :
-- Use Interactive Rebase : **git rebase i HEAD~25**
-- Keep The First commit as pick and change the remaning 24 commits from pick to squash(or s)
-- Then Save ,provide the final commit message, and complete the rebase.
-- Push the updated history: **git push --force-with-lease**

## Q : 
- You raised a PR.
- Reviewer requested changes.
- How will you update the PR?
Ans : 
-- Make The Requested changes on your branch.
-- Commit the Changes :
    git add.
    git commit -m "address review comments"
-- Push The Changes : git push
-- The PR gets updated automatically.

## Q : 
- A PR has conflicts with main branch.
- What will you do?
Ans : 
-- Update your branch with the latest changes from main:
    - Rebase 
    - Merge

## Q : 
- Your PR accidentally contains 100 unrelated file changes.
- How would you clean it?
Ans :
-- Identify and remove the unrelated changes from the branch before merging
-- Options
    - Revert/remove unwanted file changes.
    - Create a fresh branch and cherry-pick only the required commits.
    - Use interactive rebase if commits need cleanup.

## Q : 
- You merged a PR.
- Production issue occurred.
- How would you rollback?
Ans : 
-- Revert the merge commit : **git revert -m 1 <merge-commit-hash>**
-- Then push the revert commit.


## Q : 
- You created Branch B from Branch A.
- Now Branch A got merged.
- How will you keep Branch B updated?
Ans : Rebase Branch B onto the latest main:
    git checkout B
    git fetch
    git rebase main

## Q : 
- You mistakenly committed directly to main.
- How will you move those commits to a feature branch?
Ans : 
-- Create a new branch from the current state:
    "git checkout -b feature-branch"
-- Go back to main and remove the commits: Reset or revert

## Q : 
- You need to work on two unrelated features simultaneously.
- How would you organize branches?
Ans : 
-- Create separate branches from main:
    git checkout main
    git checkout -b feature-A

    git checkout main
    git checkout -b feature-B

## Q : 
- Feature A depends on Feature B.
- How would you create branches?
Ans : 
-- Create Feature B first, then create Feature A from Feature B:
    git checkout main
    git checkout -b feature-B

    git checkout feature-B
    git checkout -b feature-A


# Conflict Resolution Scenarios
## Q : 
Two developers modified the same file.
- Merge conflict occurs.
- How will you resolve it?
Ans : 
1. Open the conflicted file.
2. Review both changes.
3. Keep the correct code (or combine both).
4. Remove conflict markers.
5. Stage and complete the merge/rebase.

## Q : Git shows: <<<<<<< HEAD ? What Does it Mean?
Ans : 
-- It indicates a merge conflict. 
    - HEAD = current branch's code
    - ======= = separator
    - >>>>>>> = incoming branch's code
-- Git is asking you to decide which code should remain.

## Q : How would you decide which code to keep during conflict resolution?
Ans : I don't choose based on Git. I choose based on the business requirement and the intended functionality, then verify the result through testing.

## Q : 
- You accidentally resolved conflict incorrectly.
- How would you fix it?
Ans : 
-- If not commited.
    git merge --abort or git rebase --abort
-- If already Commited..
    - Manaually Correct the Code 
    - The Commit with new Hash id.

# Stash Scenarios
## Q : 
- You are halfway through a feature.
- Production issue arrives.
- How will you switch branches without committing incomplete work?

## Q : 
- You created multiple stashes.
- How will you identify the correct one?

## Q : Difference In git stash apply And git stash pop ?

## Q : Can stash cause conflicts? What would you do ?

# Reflog Scenarios
## Q :
- You accidentally ran: git reset --hard
- and lost commits.
- How will you recover them?

## Q : 
- You rebased and lost history.
- What Git command helps recover it?

## Q : Difference between: git log and git reflog ?

# Reset/Revert Scenarios
## Q : 
- A bad commit is already pushed to remote.
- Would you use reset or revert?
- Why?

## Q : 
- You committed locally but haven't pushed.
- Need to remove commit.
- What would you use?

## Q : 
- Production branch contains a bad commit.
- Safest way to undo it?

## Q : Difference in git reset --soft ,--mixed ,--hard ?

# Production Release Scenarios
## Q : 
- Production release is tomorrow.
- One critical bug fix is ready.
- How would you move only that fix to release branch?

## Q : 
- Release branch and main branch diverged.
- How would you handle it?

## Q : 
- Hotfix was done directly on production branch.
- How will you bring it back to main branch?

## Q : 
- Production rollback is needed immediately.
- What options do you have?

# Collaboration Scenarios
## Q : Q37

Another developer force-pushed your shared branch.

What happens?

How will you recover?

Q38

You pulled latest code and many conflicts appeared.

How would you proceed?

Q39

Your teammate deleted a branch accidentally.

Can Git recover it?

How?

Q40

You need to review another developer's code.

What things do you check in a PR?

# GitHub Specific Scenarios
Q41

A PR is approved but CI pipeline fails.

Would you merge it?

Why?

Q42

A PR passes tests but code quality looks poor.

What would you do?

Q43

Branch protection rules prevent direct push.

Why do teams use this?

Q44

Someone force-pushes to main.

What risks exist?

Q45

A PR was merged accidentally.

How will you undo it?

Q46

You need mandatory code review before merge.

How can GitHub enforce this?

Q47

You want deployment only after PR merge.

How would GitHub Actions help?

# Advanced Senior-Level Scenarios
Q48

You have:

main
 |
 ├── feature-A
 |
 └── feature-B

Feature-B depends on Feature-A.

Feature-A is delayed.

How will you continue Feature-B development?

Q49

A branch contains 100 commits.

Only 3 should be merged.

How would you do it?

Q50

Your branch history looks like:

A-B-C-D-E-F

You want:

A-B-F

How?

Q51

You accidentally exposed a password in Git history and pushed it.

What steps would you take?

Q52

A repository became very large (5+ GB).

What Git strategies would you use?

Q53

You need to find:

"Which commit introduced this bug?"

What Git feature helps?

(Hint: git bisect)

Q54

A bug exists today but wasn't there last week.

How would you identify the exact commit responsible?

Q55

A PR contains 5000 lines changed.

As reviewer, what concerns do you have?