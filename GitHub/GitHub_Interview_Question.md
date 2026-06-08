# 1. Git Fundamentals (Must Know – 100% Asked)
## What is Git?
1. Analogy 
-- Socho tum MS Word me ek document likh rahe ho.
    - Day 1 : Document Version 1
    - Day 2 : Kuch changes kiye → Version 2
    - Day 3 : Aur changes → Version 3
-- Ab agar galti ho jaye, tum chahoge ki purane version pe wapas ja sako.
-- Aur agar team me 5 log same document pe kaam kar rahe ho, to har kisi ka change track hona chahiye.
-- Git exactly yehi karta hai   
    - Ye project ke har change ka history maintain karta hai aur multiple developers ko ek saath kaam karne deta hai.

2. Technical Explanation
-- Git ek Distributed Version Control System (DVCS) hai.
-- Iska use source code ke changes ko track karne aur manage karne ke liye hota hai.
-- Git ki help se developers:
    - Code ka history track kar sakte hain
    - Previous version pe revert kar sakte hain
    - Multiple developers ek project pe collaborate kar sakte hain
    - Different features ke liye branches bana sakte hain
-- Git fast aur lightweight hai
-- Offline bhi kaam kar sakte ho
-- Mostly GitHub / GitLab / Bitbucket ke saath use hota hai

## What is GitHub and how is it different from Git?
1. Analogy
-- Socho Git ek diary hai jisme tum apne project ke saare changes likhte ja rahe ho.
    - Tum diary me likhte ho → kya change hua
    - Kab change hua
    - Kisne change kiya
-- Lekin agar team ke 5 log ek project pe kaam kar rahe ho, to diary ko sabko share karna padega.
-- Yaha GitHub aata hai.
-- GitHub ek online place (cloud platform) hai jaha Git repository store hoti hai, taki team ke sab log internet ke through same project pe collaborate kar sake.

2. Techincal
-- Git (Tool)
    - Ek Version Control System hai
    - Local machine pe code changes track karta hai
    - Commit history maintain karta hai
    - Git bina GitHub ke bhi use ho sakta hai
-- GitHub (Platform)
    - Ek cloud-based hosting platform hai jo Git repositories ko host karta hai
    - Collaboration features deta hai:
        - Pull Requests
        - Code Review
        - Issue Tracking
        - CI/CD integration
    - Similar PlatForms : Git Lab , Bit Bucket  

## What is a repository in GitHub?
1. Analogy 
-- Socho repository ek project folder jaisa hai.
-- Jaise tumhare laptop me ek folder hota hai:
    BankingApp/
    ├── Login.cs
    ├── AccountService.cs
    ├── README.md
-- Is Folder me :
    - Code files
    - Project files
    - Documentation
-- Sab stored hote hain.
👉 Git repository bhi ek project folder hi hota hai, lekin usme code ke saare changes ka history bhi store hota hai.

2. Techincal
-- Repository (Repo) ek storage location hoti hai jaha:
    - project ka source code
    - commit history
    - branches 
    - configuration files.
-- store hote hain.
-- GitHub me repository online hosted project storage hoti hai.

3. Important Commands
git init        # new repository create
git clone <url> # existing repo download

## What is the difference between local repository and remote repository?
1. Analogy
-- Socho tum ek project file apna laptop pe bana rahe ho.
👉 Local Repository
    - Tumhare laptop me stored project 
    - Sirf tum access kar sakte ho.
👉 Remote Repository
    - Same project internet pe stored hai (GitHub)
    - Team ke sab log access kar sakte hain
Matlab :
    - Local : Personal Workspace.
    - Remote : Team Shared Workspace.

2. Techincal 
-- Local Repository
    - Developer ki local machine pe stored Git repository
    - Yaha developer commits aur changes karta hai
    - Local repo me offline kaam ho sakta hai
-- Remote Repository
    - Server / cloud pe stored repository
    - Example : GitHub , GitLab , Bitbucket
    - Team collaboration ke liye use hoti hai

## What is a commit?
1. Analogy
-- Socho tum project ka kaam kar rahe ho aur har important step pe screenshot save kar lete ho.
-- Example :
    - Step 1 : Login page banaya → Screenshot save
    - Step 2 : Validation add ki → Screenshot save
    - Step 3 : Bug fix kiya → Screenshot save
-- Agar bad me problem aaye to tum pichle screenshot pe wapas ja sakte ho.
👉 Git me ye screenshot hi commit hota hai.
-- Commit matlab code ka ek saved snapshot at a particular time.

2. Techincal 
-- Commit Git me ek snapshot hota hai jo project ke changes ko permanently save karta hai.
-- Commit me ye information hoti hai:
    - Changed files
    - Author
    - Timestamp
    - Commit message
-- Har commit ka unique commit ID (hash) hota hai.
-- Good practice: clear commit message likhna.

3. Important Command
    git add .
    git commit -m "Added login validation"
-- Explanation
    - git add -> changes stage karta hai.
    - git commit -> changes repository history me save karta hai.

## What is the difference between git add and git commit?
1. Analogy
👉 git add
    -- Product ko cart me add karna
    -- Abhi purchase nahi hua
👉 git commit
    -- Place Order button dabana
    -- Ab purchase permanently ho gaya

2. Techincal
-- git add = staging 
-- git commit = saving snapshot
-- Commit sirf staged files ko save karta hai
-- Agar file add nahi ki, to commit me include nahi hogi

## What is the difference between git fetch and git pull?
1. Analogy
-- Socho team drive (Google Drive) me ek project file hai.
👉 git fetch
    - Tum sirf check karte ho ki drive me kya new changes aaye hain
    - Lekin apni file me automatically apply nahi karte
👉 git pull
    - Tum drive se latest file download karke apni file update kar lete ho
Matlab:
    - fetch = sirf updates dekhna
    - pull = updates lana + apply karna

2. Technical
-- git fetch
    - Remote repository se latest commits download karta hai(Safe Operation)
    - Lekin local branch ko update nahi karta
    - Command : **git fetch****
-- git pull
    - Remote repository se changes download karta hai aur merge bhi karta hai
    - git pull = git fetch + git merge
    - command : **git pull origin main**

## What is the purpose of git clone?
-- git clone remote repository (GitHub, GitLab etc.) ki complete copy local machine me create karta hai.
-- Command
    git clone <repository-url>

## What is the purpose of git status?
1. Analogy
-- Socho tum project pe kaam kar rahe ho aur tum check karna chahte ho:
    - kaunsi files change hui hain
    - kaunsi files commit ke liye ready hain
    - kaunsi files abhi track nahi ho rahi
👉 Ye sab check karne ke liye git status use hota hai.

2. Techincal
-- git status repository ka current state show karta hai.
-- Ye batata hai:
    - modified files
    - staged files
    - untracked files
    - current branch
--Command : **git status** 

## What is the purpose of git log?
1. Analogy
-- Socho project ka ek history register hai jisme likhe hai :
    - Kisne change kiya
    - kab change kiya
    - kya change kiya
👉 Ye register git log hai.

2. Technical
-- git log repository ki commit history show karta hai.
-- Ye Infomartion deta hai :
    - commid ID
    - author 
    - date 
    - commit message

3. Important Commands
-> git log 
-> git log --oneline

# 2. Branching Concepts
## What is a branch in Git?
1. Analogy
-- Socho tum ek book likh rahe ho
    - Main book → Original story
    - Ab tum ek new idea try karna chahte ho (alternate ending)
👉 Git me branch bhi exactly yehi karta hai.
-- Branch matlab main code se alag ek parallel line jaha new feature ya changes develop karte hain.

2. Technical
-- Branch Git me ek separate line of development hoti hai.
-- Iska use hota hai:
    - new feature develop karne ke liye
    - bug fix karne ke liye
    - experiment karne ke liye
-- Default branch usually main ya master hoti hai.
-- Developers new branches bana ke kaam karte hain aur baad me merge kar dete hain.
-- Branches parallel developement allow harti hain
-- Main branch stable code ke liye hoti hai.
-- Features mostly feature branches me develop hote hain , Baad me merge ki jati hai.

3. Important Commands
-> **git branch feature-login** → new branch create
-> **git checkout feature-login** → branch switch
-> **git checkout -b feature-login** → create + switch

## Why do we use branches?
1. Branches parallel development allow karti hain
2. Main branch stable code ke liye hoti hai
3. Features mostly feature branches me develop hote hain
4. Baad me branch merge ki jati hai

## What is the difference between main/master branch and feature branches?
👉 Main/Master Branch
    -- Project ki primary branch hoti hai
    -- Stable aur production-ready code store hota hai

👉 Feature Branch
    -- New features develop karne ke liye separate branch create ki jati hai
    -- Feature complete hone ke baad main branch me merge ki jati hai

👉 Important Commands
-> git checkout -b feature-login  (Feature branch create karna:)
-> git checkout main    (Main branch me wapas jana:)
-> git merge feature-login  (Feature branch merge karna:)

## What is git checkout vs git switch?
1. Analogy
-- Socho office me ek room hai jaha multiple desks hain.
    - Desk A → Main project
    - Desk B → Login feature
    - Desk C → Payment feature
-- 👉 Tum ek desk se dusre desk pe shift ho jate ho kaam karne ke liye.
-- Ye desk change karna = branch change karna.
-- Git me ye kaam pehle git checkout se hota tha.
-- Baad me Git ne git switch introduce kiya jo sirf branch switching ke liye simple command hai.

2. Technical
-- git checkout
    - Old command hai
    - Multiple kaam karta hai 
        - branch switch
        - new branch create
        - files restore
    - Isliya thoda confusing ho jata hai.
-- git switch 
    - New command hai 
    - Sirf branch switch karne ke liye design hua hai.
    - More clear and Safe.

3. Command
-- Branch switch 
    > git checkout feature-login
    > git switch  feature-login
-- New branch create + switch
    > git checkout -b feature-login
    > git switch -c feature-login



## What is git branch command used for?
1. Techincal
-- git branch command ka use Git branches ko manage karne ke liya hota hai.
-- Is command se hum:
    - new branch create kar sakte hain.
    - exisitng branches list kar sakte hain
    - branch delete kar sakte hain
-- Branch basically separate line of development hoti hai.

2. Important Command
-- Branch list dekhna
    > git branch
-- New branch create karna
    > git branch feature-login
-- Branch delete karna
    > git branch -d feature-login

## What is the difference between branching and forking?
1. Analogy
-- Socho company ka ek main project hai.
👉 Branching
    - Tum same project ke andar ek new working line bana lete ho
    - Jaise: login-feature, payment-feature
    - Sab kuch same project ke andar hota hai
👉 Forking
    - Tum poore project ki copy apne account me le lete ho
    - Ab tum us project ko independently modify kar sakte ho
MAtlab : 
    - Branch = same project ke andar parallel development
    - Fork = project ki full copy apne account me

2. Technical
-- Branching
    - Same repository ke andar new branch create karna
    - Mostly team development aur feature development ke liye use hota hai
    - Fast aur lightweight
-- Forking 
    - Kisi repository ki complete copy apne GitHub account me create karna
    - Mostly open source contribution ke liye use hota hai


## What is git branch -d vs -D?
1. Analogy
-- Socho tumne ek temporary working notebook banayi thi experiment ke liye.
-- Ab do Situtaion ho sakti hain :
👉 git branch -d
    - Agar notebook ka kaam complete ho chuka hai aur main notebook me merge ho gaya hai, to tum safe tarike se us notebook ko delete kar dete ho.
👉 git branch -D
    - Agar notebook merge nahi hui hai phir bhi tum force se delete kar dete ho, chahe kuch work lost ho jaye.
-- Matlab : 
    -d = safe delete
    -D = force delete

2. Techincal 
-- git branch -d
    - Branch ko safe tarike se delete karta hai
    - Delete tabhi hoti hai jab branch already merged ho chuki ho
-- git branch -D
    - Branch ko forcefully delete karta hai
    - Chahe branch merge hui ho ya nahi
    - Actually : -D = force delete (-d + force)

3. Command 
-- Safe Delete : "git branch -d feature-login"
-- Force Delete : "git branch -D feature-login"

# 3.  Merging & Rebasing
## What is git merge?
1. Analogy
-- Socho 2 developers alag-alag notebooks me kaam kar rahe hain.
    - Developer A → Main notebook
    - Developer B → Feature notebook (login feature)
-- Ab jab login feature complete ho jata hai, to developer B ke changes main notebook me add kar diye jate hain.
-- Ye notebooks ko combine karna = merge.

2. Techincal Explanation
-- git merge ka use ek branch ke changes ko dusri branch me combine karne ke liye hota hai.
-- Generally WorkFlow
    - Developer feature branch me kaam karta hai
    - Feature complete hone ke baad usse main branch me merge kar diya jata hai

3. Command
-- Main branch pe switch karo : "git checkout main"
-- Feature branch merge karo : "git merge feature-login"


## What is git rebase?
1. Analogy
-- Socho 2 developers ek hi document pe kaam kar rahe hain
    - Main document updated ho gaya
    - Tumhara feature document purane version se start hua tha
👉 Ab tum apne changes ko latest document ke upar dobara apply kar dete ho.
-- Isse history clean aur straight line me dikhti hai.
-- Yehi Rebase hai.

2. Techincal
-- git rebase ek process hai jisme ek branch ke commits ko dusri branch ke latest commit ke upar replay kiya jata hai.
-- Isse :
    - History linear ho jati hai
    - unnecessary merge commits avoid hote hain

3. Important Commands
> git fetch
> git Checkout main
> git pull origin main
> git checkout featurebranch
> git rebase main
> (--continue , --abort...)
> git push --force


## Difference between merge vs rebase?
1. Analogy
-- Socho 2 notebooks hain.
👉 Merge
    - Dono notebooks ko combine kar dete ho
    - Aur ek new page add ho jata hai jisme likha hota hai combine
👉 Rebase
    - Tum apne notes ko latest notebook ke upar dubara likh dete ho
    - History straight line me ho jati hai

2. Techincal
| Feature                | Merge                        | Rebase          |
| ---------------------- | ---------------------------- | --------------- |
| History                | Non-linear                   | Linear          |
| Extra commit           | Merge commit create hota hai | No merge commit |
| Safe for shared branch | Yes                          | Risky           |

3. Important
-- Use Merge When
    - shared branches
    - team collaboration
-- Use Rebase When
    - clean history chahiye
    - feature branch update karni ho

## What is a merge conflict?
1. Analogy
-- Socho 2 developers same line edit kar dete hain.
-- Example :
    - Dev A : Price = 100;
    - Dev B : Price = 120;
-- Ab Git confuse ho jati hai kaunsa change correct hai,
    - Is situation ko merge conflict kehte hain.

2. Techincal
-- Merge conflict tab hota hai jab Git automatically decide nahi kar pata ki kaunsa change apply kare.
-- Usually conflicts hote hain jab:
    - Same File ,
    - Same Line ,
    - Different Changes.

## How do you resolve merge conflicts?
1. Analogy
-- Socho 2 log ek document me different changes kar dete hain.
-- Ab tum manually decide karte ho kaunsa change correct hai aur final version save kar dete ho.
-- Yehi conflict resolution hai.
.................
3. Techincal Steps 
    -- Git file me conflict markers show karta hai:
        <<<<<< HEAD
        price = 100
        =======
        price = 120
        >>>>>>> feature-branch
    -- Developer ko correct code select karke markers remove karne hote hain.

## What is fast-forward merge?
1. Analogy
-- Socho tum ek notebook me kaam kar rahe ho.
    - Main notebook : Page 1 -> Page 2
    - Feature Notebook : Page 1 -> Page 2 -> Page 3 -> Page 4
-- Ab jab feature complete ho jata hai aur main notebook me koi new change nahi hua, to tum simply main notebook ko Page 4 tak forward kar dete ho.
-- Koi Extra combine page nahi banta 
-- Yehi Fast - Forward Merge hai.

2. Technical
-- Fast-forward merge tab hota hai jab target branch me koi new commits nahi hote aur Git simply branch pointer ko aage move kar deta hai.
-- Is Case Me : 
    - Koi merge commit create nahi hota 
    - history linear rethi hai.

3. Example 
-- Before Merge
   main:     A --- B
                    \
   feature:         C --- D
-- After Fast - Forward Merge 
    main : A --- B --- C --- D
-- Git simply main pointer ko D tak move kar deta hai.


## What is squash merge?
1. Analogy
-- Socho tum feature pe kaam karte waqt 10 chhote-chhote notes likh dete ho:
    - Fix Type
    - Update button color
    - Small bug fix
    - Change API Call
-- Ab jab Feature complete ho jati hai , Tum in sab notes ko ek single clean note me summarize kar dete ho:
    "Add Complete login feature"
-- Ye sab commits ko ek commit me convert karna = squash merge.

2. Technical
-- Squash merge me ek branch ke multiple commits ko combine karke ek single commit bana diya jata hai jab usse target branch me merge karte hain.
-- Result :
    - Feature branch ke multiple commits → 1 commit
    - Project history clean aur simple ho jati hai.

3. Example :
-- Before Squash 
    main:     A --- B
                \
    feature:        C --- D --- E --- F
-- After squash merge
    main: A --- B --- G
👉 Yaha C, D, E, F → ek commit G ban gaya.

# 4. Commits & History Management
## What is the difference between: git reset and git revert
git reset
1. Analogy git reset 
-- Socho tum notebook me 5 steps likh chuke ho.
-- Agar tum step 5 aur 4 ko completely erase karke notebook ko step 3 tak wapas le jao, to kya hoga?
-- Future ke steps history se hi remove ho jayenge
-- ye git reset jaisa hai.

2. Technical git reset 
-- git reset ka use repository ko kisi previous commit par move karne ke liye hota hai.
-- Isme : 
    - current branch pointer pichle commit pe shift ho jata hai
    - newer commits history se remove ho sakte hain

3. Important git reset 
-- Exammple : "git reset --hard HEAD~1"
-- Meaning : Last commit remove ho jayega.
................
git revert
1. Analogy
-- Socho notebook me step 5 galat likh diya.
-- Lekin tum usse erase nahi karte.
-- Tum ek new step likh dete ho jo step 5 ko undo kar deta hai.
-- Matlab history safe rethi hai.
-- Ye git revert hai.

2. Technical
-- git revert ek new commit create karta hai jo previous commit ke changes ko undo kar deta hai.
-- Important
    - Old commit delete nahi hota
    - History safe rethi hai.

3. Important Command
git revert <commit-Id>
.........................
Difference In git revert and git reset
| Feature       | git reset        | git revert     |
| ------------- | ---------------- | -------------- |
| History       | Rewrite hoti hai | Safe rehti hai |
| Commit delete | Yes              | No             |
| New commit    | No               | Yes            |
| Use case      | Local changes    | Shared repo    |

## What is git amend?
1. Analogy
-- Socho tumne notebook me ek entry likhi: "Add Login Feature"
-- Baad me tumhe pata chala:
    - commit message galat hai
    - ya ek file add karna bhool gaye
-- Ab tum new entry likhne ke bajaye usi last entry ko edit kar dete ho.
👉 Ye last entry ko modify karna = git amend.

2. Techincal
-- git commit --amend ka use last commit ko modify karne ke liye hota hai.
-- Isse Tum :
    - last commit message change kar sakte ho
    - last commit me extra changes add kar sakte ho
-- Important: Ye last commit ko replace kar deta hai
-- Sirf last commit modify hota hai
-- New commit create nahi hota
-- Commit rewrite ho jata hai
-- Shared branch me carefully use karna chahiye

3. Important Commands
-- Commit message change karna  : "git commit --amend -m "Updated login feature""
-- Last Commit me new changes add karna :
    "git add login.cs"
    "git commit --amend"

## What is git cherry-pick?
1. Analogy
-- Socho 2 NoteBooks hain
    - Notebook A → Main project
    - Notebook B → Feature work
-- Notebook B me 10 changes likhe hain, lekin tumhe sirf ek specific change chahiye.
-- To tum sirf wahi ek line copy karke main notebook me add kar dete ho.
👉 Ye specific commit ko copy karna = git cherry-pick.

2. Techincal
-- git cherry-pick ka use ek specific commit ko ek branch se uthakar dusri branch me apply karne ke liye hota hai.
-- Matlab : 
    - Puri branch merge nahi hoti
    - Sirf selected commit apply hota hai

3. Important
git switch Branch_name
git cherry-pick <commit-id>

## What is git reflog?
1. Analogy
-- Socho tum notebook me kaam kar rahe ho aur galti se kuch pages delete ho gaye.
-- Normal history me wo pages nazar nahi aate, lekin tumhare paas ek hidden activity log hai jisme likha hai:
    - kab page add hua
    - kab delete hua
    - kab change hua
-- Is log ki help se tum lost page wapas la sakte ho
👉 Git me ye hidden activity log = git reflog.

2. Techincal
-- git reflog repository ke HEAD aur branch references ka history track karta hai.
-- Ye Batata Hai : 
    - branch kab move hui
    - reset kab hua
    - rebase kab hua
    - commits kab change hue
-- Iske Help se lost commits recover kiya ja saktea hain.
-- Git ka safety log hai
-- Lost commits recover karne me help karta hai
-- Reset / rebase ke baad bhi commits mil sakte hain
-- Default 90 days tak history store hoti hai

3. Important Command
> git reflog

## What is git stash?
1. Analogy
-- Socho tum project pe kaam kar rahe ho, lekin kaam abhi complete nahi hua.
-- Achanak manager bolta hai: "Pehle ek urgent bug fix karo."
-- Ab tum current incomplete work ko temporarily side me rakh dete ho aur bug fix karne lagte ho.
-- Baad me wapas us work ko resume kar lete ho.
👉 Git me ye temporary save karna = git stash.

2. Techincal 
-- git stash ka use current uncommitted changes ko temporarily store karne ke liye hota hai.
-- Ye : 
    - Working directory ko clean kar deta hai.
    - changes ko stash stack me store kar deta hai
-- Baad me developer stash ko wapas apply kar sakta hai.
-- Temporary Storeage hota hai.
-- Commit create nahi hota
-- Multiple stashes stack me store ho sakte hain
-- Urgent branch switch ke time usefull hota hai.

3. Commands 
-- Changes stash karna : "git stash"
-- Stash list dekhna : "git stash list"
-- Stash apply karna : "git stash apply"
-- Stash apply + remove : "git stash pop"


## When should you use git stash?
1. Analogy
-- Socho Tum Feature develop kar raho ho , lekin
    - kaam incomplete hai
    - commit karna nahi chahte
-- Aur tumhe branch switch karna hai.
-- To tum work ko temportary stash kar dete ho.

# 5. Collaboration Using GitHub
## What is a Pull Request (PR)?
1. Analogy
-- Socho tum company me kaam kar rahe ho.
    - Tumne apni feature branch me Login Feature complete kar diya.
    - Lekin tum directly main branch me code nahi daal sakte
-- Tum manager ko bolte ho:
    "Maine changes kar diye hain. Please review karo aur agar sab sahi hai to main project me add kar do."
-- yahi Pull Request Hai.

2. Technical Explanation
-- Pull Request (PR) GitHub ka ek feature hai jiske through developer apni branch ke changes ko kisi dusri branch (usually main) me merge karne ki request karta hai.
-- PR me team:
    - Code Review karti hai
    - Suggestions deti hai
    - Discussion karti hai
    - Approve ya Reject karti hai
-- Approval ke baad PR merge hota hai.
-- PR Git ka nahi, GitHub/GitLab/Bitbucket ka feature hai
-- Code Review ke liye use hota hai
-- Team collaboration improve karta hai
-- Direct commits to main branch avoid karne me help karta hai
-- PR me comments aur discussions ho sakti hain

## What is the purpose of code reviews in PR?
- Techincal
-- Code Review ek process hai jisme team members Pull Request ke code ko review karte hain before merge.
-- Purpose
    - Bugs identify karna
    - Code quality improve karna
    - Coding standards maintain karna
    - Knowledge sharing karna
    - Security issues detect karna

## What is a fork in GitHub?
1. Analogy
-- Socho kisi ne GitHub par ek project upload kiya hai.
-- Tum us project me contribution karna chahte ho, lekin tumhare paas us repository ka write access nahi hai.
-- To Tum : 
    - Project ki apne account me copy bana lete ho
    - Us copy me changes karte ho
    - Fir original owner ko PR bhejte ho
-- Ye copy banana = Fork kehlata hai.

2. Techincal
-- Fork GitHub ka feature hai jo kisi repository ki copy tumhare GitHub account me create karta hai.
-- Fork Karne ke Baad
    - Tum independently changes kar sakte ho
    - Original repository affect nahi hoti
    - Baad me Pull Request ke through contribution kar sakte ho
-- Fork GitHub feature hai, Git command nahi
-- Mostly Open Source Projects me use hota hai
-- Original repository se separate copy banti hai
-- Changes automatically original repo me nahi jate

## What is the difference between fork and clone?
1. Analogy
-- Socho ek project GitHub par pada hai.
-- Fork : Tum project ki copy apne GitHub account me banate ho.
-- Clone : Tum project ko GitHub se apne laptop me download karte ho.

2. Techical
| Fork                             | Clone                          |
| -------------------------------- | ------------------------------ |
| GitHub feature                   | Git command                    |
| GitHub account me copy banti hai | Local machine me copy aati hai |
| Open-source contribution ke liye | Development ke liye            |
| Remote to Remote                 | Remote to Local                |


## How do you contribute to an open-source project using GitHub?
1. Analogy
-- Socho kisi ne public project banaya hai.
-- Tum directly uski notebook edit nahi kar sakte.
-- To : 
    - Copy banao (Fork)
    - Apni copy me changes karo
    - Owner ko review ke liye bhejo (PR)

2. Technicals
Fork Repository
      ↓
Clone Fork
      ↓
Create Branch
      ↓
Make Changes
      ↓
Commit & Push
      ↓
Create Pull Request
      ↓
Code Review
      ↓
Merge

3. Commands
git clone <fork-url>
git checkout -b feature-fix
git add .
git commit -m "Fixed bug"
git push origin feature-fix

## What are GitHub Issues?
GitHub Issues project me bugs, tasks, feature requests aur improvements ko track karne ke liye use hote hain. Ye project management aur collaboration ko improve karte hain.

## What are GitHub Discussions?
GitHub Discussions ek forum-like feature hai jo project contributors aur users ko questions, ideas, feedback aur general discussions karne ki facility deta hai. Ye Issues se alag hai kyunki Discussions ka focus conversation par hota hai, task tracking par nahi.

# 6. Access Control & Permissions
What are GitHub collaborators?
What are GitHub teams and organizations?
What is branch protection rule?
What is required status check in GitHub?

# 7. GitHub Workflow & CI/CD
What is GitHub Flow?
What is Git Flow?
What are GitHub Actions?
What is CI/CD pipeline in GitHub?
How do GitHub Actions automate builds and tests?
What is a workflow file in GitHub Actions?

# 8. Advanced Git Concepts
What is a detached HEAD state?
What is submodule in Git?
What is monorepo vs multirepo?
What is git bisect?
What is git tag?
Difference between lightweight tag vs annotated tag?

# 9. Large Scale Repository Management
What is Git LFS (Large File Storage)?
Why is Git not ideal for large binary files?
How does GitHub handle large repositories?

# 10. Debugging & Troubleshooting
How do you undo a commit?
How do you remove a file from Git history?
What happens if you accidentally push sensitive data?
How do you fix a broken commit history?

# 11. Real Production Questions (Very Common)
How do you manage multiple developers working on the same project?
How do you enforce code review policies?
How do you manage release versions using GitHub?
How do you maintain clean commit history?
What branching strategy do you use in production?

# 12. System Design / Architecture Questions
Design a Git workflow for a large engineering team
How would you handle 100 developers working on the same repository?
How would you manage hotfixes in production?
How would you design a CI/CD pipeline using GitHub Actions?
How do companies manage microservices repositories using GitHub?
