# Git Basics Interview Questions For GFG
## 1. What Is Git?
1. Defination
Git ek Version Control System (VCS) hai jo code ke changes ko track karta hai.
👉 Simple words me:
Git = Code ka history manager + backup system + collaboration tool
    - Har change ka record rakhta hai
    - Multiple developers ko saath kaam karne deta hai
    - Old version pe wapas ja sakte ho anytime

2. Trading Firm Example
-- Soch ek Trading Firm hai jahan ek trading system develop ho raha hai:
    - Tumhari team ne ek Order Matching Engine banaya
    - Fir kisi ne usme change kiya (latency improve karne ke liye)
    - Fir kisi aur ne risk calculation add ki
    👉 Ab problem:
    - Kaunse version me bug aaya?
    - Kaunse version stable tha?
    - Kisne kya change kiya?
    💡 Yahin Git ka kaam aata hai:
-- Git = Trading System ka Audit Trail + Version History
-- Jaise trading me har order ka log hota hai:
    - Kis time pe order aaya
    - Kisne place kiya
    - Kya price tha
    👉 Waise hi Git me:
    - Kisne Code Change Kiya
    - Kab Kiya
    - kya Change Kiya

3. Some Feature
-- Internet ke bina bhi kaam kar sakta hai
-- Har developer ke paas full code + history hoti hai
-- Naye features try karo bina main code ko todhe
-- Agar trading system crash ho gaya, turant old stable version pe ja sakte ho
-- Multiple traders (developers) ek hi system pe kaam kar sakte hain

## 2. What is a repository in Git?
1. Defination
-- Repository (repo) ek project ka storage place hota hai jahan:
    - Saara code store hota hai
    - Saari history (commits) save hoti hai
    - Changes track hote hain
👉 Simple:
Repository = Project ka full folder + uski history

2. Trading Firm Example
-- Soch ek Trading Firm ka Core System hai -- jaise :
👉 "Equity Trading Platform"
-- Isme Kya kya hoga :
    - Order Placement module
    - Risk Management
    - Market data handler
    - Logs and configs
💡 Ye poora system ek Repository hai
🔍 Real Scenario:
-- Tumhari firm me ek repo hai:
👉 trading-system-repo
-- Is repo me:
Har file = system ka ek part
Har change = ek update (jaise new risk rule)
Har version = system ka ek snapshot

3. Mapping
-> Repo : Trading System (poora setup)
-> Files : Modules (Order , Risk , Pricing)
-> Commits : System updates / releases

## 3. What is the difference Between Git and GitHub?
-> Git :
-- Git ek tool (software) hai
-- Code ko track , manage aur version control karta hai
    👉 Runs on your local machine

-> GitHub : 
-- GitHub ek platform (website/service) hai
-- Jahan tum apna Git repo store & share karte ho
    👉 Works on internet (cloud)

## 4. What is Origin in Git?
1. Defination
👉 Origin ek default naam (alias) hota hai jo Git me use hota hai remote repository ke liye.
    - Jab tum GitHub (ya kisi server) se repo connect karte ho
    - Git automatically uska naam rakh deta hai: origin
👉 Simple:
Origin = Tumhara main remote repo ka shortcut naam

2. Trading Firm Example
-- Soch ek Trading Firm hai:
-- Tum apne system pe kaam kar rahe ho (local system),
-- aur ek central trading server hai jahan sabka code store hota hai.
-- Scenario
    - Tum apne laptop pe trading logic update karte ho
    - Fir tum usko central server pe bhejte ho
    👉 Ye central server = origin

3. Important
-- Origin sirf ek naam hai (default) , It Can be Changed
-- Remote Repo ka reference hai

## 5. What is the Purpose of the .gitihnores files ?
1. Defination
👉 .gitignore ek file hoti hai jisme hum define karte hain:
Kaun kaun si files/folders Git ko track nahi karni chahiye

2. Trading Example
-- Soch ek Trading Firm ka system hai:
-- System me 3 types ki cheezein hain:
    1. ✅ Important:
        - Trading logic code
        - Risk rules
        - Order engine
    2. ❌ Unnecessary:
        - Temporary logs
        - Cache files
        - Local configs
    3. Sensitive
        - API Keys
        - DB Passwords
-- Scenario
    - Tumhari team ne galti se:
        - logs/ folder
        - temp files
        - config with password
    - Git me Dal Diya
    - Is sa problem ya hogi 
        - Repo Heavy 
        - Security Risk
        - Team me unnecessary files share ho rahi hain
-- Solution = .gitignore  

3. Important
-- Sensitive Data Protect karta hai
-- Repo Clean rakhta hai
-- Performance Improve

4. 👉 Agar file already commit ho chuki hai
-- .gitignore usko ignore nahi karega
-- useka liya : "git rm --cached file_name"


## 6. What is a version control system (VCS)?
1. Defination
👉 Version Control System (VCS) ek system hai jo:
    - Code ke har change ko track karta hai
    - Different versions maintain karta hai
    - Old version pe wapas jaane deta hai
👉 Simple:
VCS = Code ka “time machine + history tracker”

2. Trading Firm Example 🏦
-- Soch ek Trading Firm hai jahan ek Trading Algorithm chal raha hai:
-- Real Scenario
    - Day 1: Algo v1 → Basic buy/sell logic
    - Day 5: Risk management add kiya
    - Day 10:  Algo v3 → Speed optimize ki
-- Problem aaya:
    - v3 me bug aa gaya → losses ho rahe hain
    - Ab kya kare?
-- Without VCS
    - Pata nahi kaunsa version stable tha
    - Code manually rollback karna padega (risk)
-- With VCS
    - Tum easily bol sakte ho:
    - Mujhe v2 pe wapas jana hai
    -  Tum dekh sakte ho:
        - Kisne change kiya
        - Kab kiya
        - Kyu kiya
    
3. Important Points
-- Collaboration Easy : Multiple developers ek hi system pe kaam kar sakte hain
-- Backup + Safety : Code kabhi lost nahi hota
-- Branching Support : Naye features safely test kar sakte ho
-- Audit Trail : Har change ka record (like trade logs)

## 7. What is the git push command?
1. Defination
👉 git push ka use hota hai:
Apne local changes (commits) ko remote repository (GitHub / origin) pe bhejne ke liye
👉 Simple:
git push = “Mera code server pe upload kar do”

2. Command : "git push origin main"

3. Real Flow...
-- git add . 
-- git commit -m "Commit This Message"
-- git push origin main

## 8. What is the git pull and fetch command?
1. Defination
👉 git pull ka use hota hai:
Remote repository (GitHub / origin) se latest changes apne local system me lane ke liye

2. Command : "git pull origin main"

3. Safe Work Flow..
-- "git fetch"
-- "git pull origin main"
-- Code Changes
-- "git add ."
-- "git commit -m "update""
-- "git push origin main"

## 9. What does git Clone do?
1. Defination
-- Remote repository (GitHub/origin) ki poori copy apne local system me lane ke liye
-- Isme sirf code hi nahi, balki:
    - Complete history
    - Branches
    - Commits
-- Sab kush aa jata hai. 

2. Command : "git clone https://github.com/company/trading-system.git"


## 10. What are the advantages of using GIT?
-- Multiple Dev can work on same project together.
-- Each developer has a local copy of the repository, improving performance and enabling offline work.
-- Free and widely supported.
-- Git supports work on various types of projects.
-- Each repository has only one Git directory.


## 11. What is the difference between git init and git clone?
-> "git init" : develops a new , empty Git repository in the present directory.
-> "git clone <url>" : Clone a remote repo locally , With history , code , all files.

## 12. What is git add ?
-> "git add ." : Add all the changes , Files to Stage (include)
-> "git add FileName" : Add Specified File to Stage (Include)

## 13. What is git status ?
1. Defination
👉 git status ek command hai jo batata hai:
    Abhi tumhare repo ki current condition kya hai
    - Kaunse files modified hain
    - Kaunse staged hain
    - Kaunse untracked hain
👉 Simple:
git status = “Mere code ki current situation batao”

2. Command : "git status"

3. Output kya batata hai:
🔴 Modified files → jo change hue hain
🟢 Staged files → jo commit ke liye ready hain
⚪ Untracked files → nayi files (Git track nahi kar raha)

## 14. What is a commit in Git ?
1. Defination
👉 Commit ek snapshot (photo) hota hai tumhare code ka at a specific point in time.
    - Jo changes tumne kiye → unko permanently save karta hai
    - Har commit ka ek unique ID hota hai
👉 Simple:
Commit = “Code ka saved version + message”

2. Command : "git commit -m "Added Risk Code""


## 15. What is the purpose of the git clean command ?
1. Defination
👉 git clean ka use hota hai:
    Untracked files (jo Git track nahi kar raha) ko delete karne ke liye
👉 Simple:
    git clean = “Repo me pade unwanted / extra files ko hata do”

2. Command : "git clean -f"
-- “Saare untracked files delete kar do”
-- Dangerous

3. Command : "git clean -n"
-- Sirf dikhayega kya delete hoga (safe)

4. Command : "git clean -fd"
-- Directories bhi delete karna ho toh

## 16. What is 'conflict' in git?
-> Git usually manages merges automatically, but conflicts occur when two branches edit the same line or when one branch deletes a file that another edits.

## 17. What is the meaning of 'Index' in GIT?
1. Defination
-- Index ko Git me "Staging Area" bhi bolta hain
-- Ye ek temporary area hai jahan hum changes ko commit karne se pehle ready rakhte hain
👉 Simple:
Index = “Commit se pehle ka waiting area”

## 18. How do you change the last commit in git?
1. Defination
-- Last commit ko change karne ke liye use hota hai:
-- Isse tum:
    -- Last commit ka message change kar sakte ho
    -- Ya usme new changes add/remove kar sakte ho
-- Simple: Ya usme new changes add/remove kar sakte ho

2. Commands: "git commit --amend"


## 19. What is `git checkout`?
-> git checkout help us to switch between  branches , created new branch, switch to remote branch

## 20. How do you switch branches in Git?
"git checkout branchname" or "git switch branchname" -> Switch To Local
"git checkout -b branch origin/branch" or "git switch -c branch origin/branch" -> Switch to Remote
"git checkout -b branch" or "git switch -c branch" -> Create new Branch

## 21 : Name Some popular Git Hosting services?
-> GitLab , GitHub , VSCode Oline , Bitbucket

## 22 : What are the different types of Git repositories?
1. Defination
🔹 Non-Bare Repository
-- Ye normal repo hota hai jisme:
    - Code files hoti hain
    - Working directory hoti hai
    - Tum directly code edit kar sakte ho
-- Simple : Non-bare = Developer ka working repo
.....
🔹 Bare Repository
-- Isme : 
    - Sirf Git data hota hai (no working files)
    - Code edit nahi kar sakte
    - Mainly sharing / central server ke liye use hota hai
-- Simple : Bare = Sirf storage repo (no direct editing)

2. Trading Firm Example
Soch ek Trading Firm hai jahan system develop ho raha hai:
🔹 Non-Bare Repo = Developer Terminal
    -- Har developer ke paas apna system hai
    -- Wo code likh raha hai
    -- Test kar raha hai
    -- Changes commit kar raha hai
👉 Ye hai Non-bare repo (BNDTRD-AMIT)
......
🔹 Bare Repo = Central Trading Server
    -- Ye ek central server hai
    -- Yahan koi directly code edit nahi karta
    -- Sab log yahan:
        -- push karte hain
        -- pull karte hain
👉 Ye hai Bare repo (UAT)    


## 23 : How does Git handle file deletion?
-> "git rm --cached <file_name>"

## 24 : How can you create an alias in Git?
-> Alias ka use Large Git commands ko Chote krna ka liya hota.
"git config --glbal alias.<alias_name>'<git_command>'"

## 25 : How do you rename a branch in Git?
-> git branch -m <new_branch_name> : Rename Current Branch
-> git branch -m <old_branch_name><new_branch_name> : Different Branch

## 26 : What is the difference between git fetch and git pull?
-> git fetch : git fetch retrieves updates from the remote repository but does not merge them into the local branch, allowing you to review changes before integrating.
-> git pull : git pull fetches updates from the remote repository and immediately merges them into the current local branch (equivalent to git fetch followed by git merge).

## 27 : Explain Git rebase and when do you use it?
1. Defination
👉 Git Rebase ka matlab hai:
    Apni branch ke commits ko uthake kisi dusri branch ke latest commits ke upar “replay” karna
👉 Simple:
Rebase = “Apni changes ko latest base ke upar shift kar dena (clean history ke saath)”

2. Example :
-- Soch ek Trading Firm hai:
    - main branch = Live trading system
    - Tumhari branch = New feature (e.g., new risk engine)
-- Scenario:
-- Day 1: 
    - Tumne branch banayi
    - Kaam start kiya
-- Day 5 : 
    - main branch me dusre devs ne
    - Bugs Fex
    - Performace Imporvement Kiya
👉 Ab tumhari branch old base pe hai
❌ Without Rebase:
    - Direct merge karoge → history messy
    - Confusing commits
✅ With Rebase:
    - "git checkout feature-branch"
    - "git rebase main"
👉 Matlab:
    - Tumhare commits ko uthake
    - Latest main ke upar rakh diya


## 28 : How will you create a git repository?
1. Donload Git on your system
2. Create a Project in the location where you want your repository.
3. Open Terminal or Command Prompt.
4. Run 'git init.'

## 29 : What differentiates between the commands git remote and git clone?
1. git remote : git remote manages connections to remote repositories. It lets you add, remove, and view remotes linked to a local project, but it does not download any files.
2. git clone : git clone creates a local copy of an existing remote repository, including all files, branches, and commit history, so you can start working immediately.

## 30 : What are the benefits of using a pull request in a project?
1. Code Review 
2. Collaboration
3. Version Control

## 31 : What is a Git bundle?
1. Defination
👉 Git Bundle ek tarika hai jisme:
    Poora Git repository (ya uska kuch part) ek single file me pack karke share kiya jata hai
    - Ye ek .bundle file hoti hai
    - Offline sharing ke liye use hoti hai
👉 Simple:
Git Bundle = “Repo ka zip file (with full history)”

2. Trading Firm Example
-- Soch ek Trading Firm hai jahan:
    - Tum ek secure environment me kaam kar rahe ho
    - Internet allowed nahi hai 🔒
    - GitHub access bhi blocked hai
-- Problem: Tumhe apna Trading System code dusri team ko dena hai , No GitGub , No Network
-- Solution : Git Bundle

3. Real Scenario
-- Tum bolte ho: 👉 “Main poora repo ek file me pack karke deta hoon”
-- Commands : "git bundle create trading.bundle --all"
            - Trading.bundle = poora repo + history
-- Dusri team : "git clone trading.bundle"



## 32 : What are the advantages of Git over SVN?
1. Git -> Distributed Version Control , each dev has it own copy , main copy secure
   SVN -> Centralized model.
2. Git -> Faster Proformance  due to local operation
   SVN -> requires netwrk communcation for many actions.
3. Git -> Branches and Merging lightweigth and eddective
   SVN -> Heavy and more complex
4. Git -> Can work offline ,
   SVN -> Dont
5. Git -> Better Conflict Resolve Tool ,
   SVN -> Not better then GIT

## 33 : What is git stash?
-> The git stash is a command used to temporarily save changes that are not yet ready to be committed. It allows developers to switch branches or work on something else without losing their progress. Stashed changes can be reapplied later using git stash pop or git stash apply.

-> Commands 
    - Save Current changes : "git stash"
    - View stashes : "git stash list"
    - Reapply the most recent stash and remove it from stash history : "git stash pop"
    - Reapply a stash without removing it from history : "git stash apply"
    - Delete a specific stash : "git stash drop stash@{n}"


## 34 : How do you revert a commit that has already been pushed and made public?
1. Checkout the Branch: Switch to the branch where you want to revert the commit.
ommands: git checkout <branch-name>

2. Find the Commit to Revert: Use 'git log' to find the commit hash of the commit you want to revert.
Commands: git log

3. Revert the Commit: Use 'git revert' followed by the commit hash of the commit you want to revert.
Commands: git revert <commit-hash>

## 35 : Explain the difference between reverting and resetting?
1. Defination
🔹 git reset
    👉 History ko peeche le jata hai (rewrite karta hai)
        - Commits remove ho jate hain (local se)
        - Dangerous ho sakta hai
    👉 Simple:
    Reset = “Past ko change karna”
🔹 git revert
    👉 Ek naya commit banata hai jo previous change ko undo karta hai
        - History safe rehti hai
        - Team-safe command
    👉 Simple:
    Revert = “Galti ko reverse karna without deleting history”

## 36 : What is the difference between git reflog and log?
1. Defination
🔹 git log
    👉 Commit history dikhata hai (official history)
        - Branch ke commits
        - Clean , Visible timeline
    👉 Simple: git log = “Project ki official history”
🔹 git reflog
    👉 HEAD aur branch movements ka record dikhata hai
        - Reset, rebase, checkout sab track hota hai
        - Even deleted commits bhi mil sakte hain
    👉 Simple: git reflog = “Hidden activity log / recovery log”

2. Trading Firm
-- Soch ek Trading Firm hai
🔹 git log = Official Trade Book 📊
        - Sirf valid trades dikhte hain
        - Final executed transactions
    Example : 
        - Buy Order
        - Sell Order
        - Final System Upates
    ✔️ Clean
    ✔️ Auditable
🔹 git reflog = Internal Activity Log 🧾
    - Sab kuch track hota hai:
        - Order Place Kiya
        - Cancel Kiya
        - Modify Kiya
        - System RollBack hua
    👉 Even: Deleted trades ka trace bhi mil sakta hai 
    ✔️ Recovery ke kaam aata hai
    ✔️ Hidden/internal tracking

## 37 : What is the HEAD in Git?
-> HEAD in Git is a reference to the latest commit on the currently checked-out branch.
-> It determines which commit and branch you are working on.
-> When switching branches, HEAD updates to point to the latest commit of the new branch.
-> If in a detached HEAD state, it means you are working on a specific commit instead of a branch.

## 38 : What is the purpose of 'git tag -a'?
1. Defination
👉 git tag -a ka use hota hai:
    Annotated tag create karne ke liye (with extra information)
Isme Hote Hai :
    - Tag name
    - Message
    - Author info
    - Date
👉 Simple:
git tag -a = “Important version ko proper label + details ke saath mark karna”

2. Example :
Soch ek Trading Firm hai:
Tumne ek stable trading system release kiya 🚀
    - Version 1.0 → Live gaya
    - Sab kuch tested & approved
👉 Ab tum chahte ho:
    - Is version ko clearly mark karo
    - Future me easily identify ho

3. Command : "git tag -a v1.0 -m "Stable Trading release v1.0""
👉 Matlab:
    - Ye version officially mark ho gaya
    - Saath me description bhi add ho gayi
-- Push annotated tags to a remort repository
"git push origin v1.0"

## 39 : What is the difference between 'HEAD', 'working tree' and 'index' in Git?
-> HEAD : reference/Point To current commit/Branch -> Located in .git/HEAD
-> Working Tree : directory where your project files are -> loacl Project directoy
-> Index : Staging Area -> Loacted in .git/index 

## 40 : How to resolve a conflict in Git?
-> To resolve a conflict in Git
    - Identify Conflict: Git will alert you of a conflict during merge or rebase.
    - Open the Conflicted File: You'll see conflict markers like <<<<<<< HEAD, =======, and >>>>>>>.
    - Resolve the Conflict: Edit the file to keep your changes, the incoming changes, or a combination of both.
    - Stage the Resolved File: Use git add <file> to mark the conflict as resolved.
    - Commit the Changes: Run git commit to complete the merge.
    - Continue Rebase (if applicable): Use git rebase --continue if you were rebasing.

## 41 : Explain the difference between 'git merge' and 'git rebase' and when you would use each?
-> git merge combines two branches and creates a merge commit
   git rebase reapplies commits from one branch on top of another

-> git merge Preserves both branches’ histories and structure
   git rebase Rewrites commit history to make it linear

-> git merge Result in Merge commit
   git rebase Creates a clean, straight history without merge commits

-> Common in collaborative environments
   Useful for personal branches and cleanup before pushing

## 42 : What language is used in GIT?
-> c.

## 43 : How do you add a file to the staging area?
-> git add .
-> git add filename

## 44 : What is git diff?
-> git diff ka use hota hai: Code me hue changes ko compare karne ke liye
    - Line-by-line difference dikhata hai
    - Kya add hua (+)
    - Kya remove hua (−)
-> Simple: git diff = “Code me kya change hua hai uska comparison”

## 45 : What is a Git commit hash?
-> unique identifier (SHA-1) for each commit 
-> helps to reference and track specific commits in the repository
-> can use it to check out or reset to a particular commit.

## 46 : What is a detached HEAD state?
-> detached HEAD state occurs when you check out a specific commit rather than a branch.
-> In this state, commits are not attached to any branch, meaning they may be lost if not properly managed.

## 47 : How can you delete a remote Git branch?
-> "git push origin --delete <branch_name>"

## 48 : What is the purpose of got cherry-pick?
-> 👉 git cherry-pick ka use hota hai:
Kisi specific commit ko ek branch se uthake dusri branch me apply karne ke liye
👉 Simple:
Cherry-pick = “Sirf ek particular change ko copy karke dusri branch me lana”

-> Command : git cherry-pick <commid-id>


## 49 : What does git ls-files do?
-> List Out all the Files that are Currently tracked By git

## 50 : How do you fetch all remote branches?
-> git fetch -all

# Git Hub Question From ChatGpt
## Git Fundamentals (Must Know – 100% Asked)
What is Git?
What is GitHub and how is it different from Git?
What is a repository in GitHub?
What is the difference between local repository and remote repository?
What is a commit?
What is the difference between git add and git commit?
What is the difference between git fetch and git pull?
What is the purpose of git clone?
What is the purpose of git status?
What is the purpose of git log?

## Branching Concepts
What is a branch in Git?
Why do we use branches?
What is the difference between main/master branch and feature branches?
What is git checkout vs git switch?
What is git branch command used for?
What is the difference between branching and forking?
What is git branch -d vs -D?

## Merging & Rebasing
What is git merge?
What is git rebase?
Difference between merge vs rebase?
What is a merge conflict?
How do you resolve merge conflicts?
What is fast-forward merge?
What is squash merge?

## Commits & History Management
What is the difference between:
git reset
git revert
What is git amend?
What is git cherry-pick?
What is git reflog?
What is git stash?
When should you use git stash?

##  Collaboration Using GitHub
What is a Pull Request (PR)?
What is the purpose of code reviews in PR?
What is a fork in GitHub?
What is the difference between fork and clone?
How do you contribute to an open-source project using GitHub?
What are GitHub Issues?
What are GitHub Discussions?

## Access Control & Permissions
What are GitHub collaborators?
What are GitHub teams and organizations?
What is branch protection rule?
What is required status check in GitHub?

## GitHub Workflow & CI/CD
What is GitHub Flow?
What is Git Flow?
What are GitHub Actions?
What is CI/CD pipeline in GitHub?
How do GitHub Actions automate builds and tests?
What is a workflow file in GitHub Actions?

## Advanced Git Concepts
What is a detached HEAD state?
What is submodule in Git?
What is monorepo vs multirepo?
What is git bisect?
What is git tag?
Difference between lightweight tag vs annotated tag?

## Large Scale Repository Management
What is Git LFS (Large File Storage)?
Why is Git not ideal for large binary files?
How does GitHub handle large repositories?
🔍 10. Debugging & Troubleshooting
How do you undo a commit?
How do you remove a file from Git history?
What happens if you accidentally push sensitive data?
How do you fix a broken commit history?
🏭 11. Real Production Questions (Very Common)
How do you manage multiple developers working on the same project?
How do you enforce code review policies?
How do you manage release versions using GitHub?
How do you maintain clean commit history?
What branching strategy do you use in production?
🧩 12. System Design / Architecture Questions
Design a Git workflow for a large engineering team
How would you handle 100 developers working on the same repository?
How would you manage hotfixes in production?
How would you design a CI/CD pipeline using GitHub Actions?
How do companies manage microservices repositories using GitHub?
🎯 13. GitHub Best Practices
Use small atomic commits
Use descriptive commit messages
Protect main branch
Use pull request reviews
Automate tests with GitHub Actions

10 GitHub Concepts Every Engineer Must Know

If you deeply understand these 10, most interviews clear ho jaate hain:

Git vs GitHub
Branching strategy
Pull requests
Merge vs Rebase
Fork workflow
Git stash
Git reset vs revert
GitHub Actions
Conflict resolution
Branch protection