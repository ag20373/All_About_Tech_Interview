# Must Know Commands
## Git New Repository Creation
-> git init        ----  # new repository create

## Git Clone a Repo
-> git clone <url> ----  # exisiting repo download.

## Git Commit Changes
-> git add .
-> git commit -m "Added login Validation"
-- Explanation:
    - git add → changes stage karta hai
    - git commit → changes repository history me save karta hai

## How To Pull from git Remote
-> git fetch origin     
-- git fetch safe operation hai , Ye sirf changes download karta hai

-> git pull origin main
-- git pull automatic merge karta hai , Pull se merge conflicts aa sakte hain

## Current Branch status
-> git status
-- git status repository ka current state show karta hai. Ye batata hai ki kaunsi files modified, staged ya untracked hain aur developer ko next action decide karne me help karta hai.

## git log
-> git log
-> git log --oneline

# Situtional Commandss