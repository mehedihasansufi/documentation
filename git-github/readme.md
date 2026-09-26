## Git & Github

### git flow 

**Working directory -- Stagging area -- local repo -- remote**
<br><br>


```md
git --version
```

### git config

```md
 git config --help
 git config user.email
 git config user.name

 <!-- for new configuration -->

git config --global user.name "Mehedi Hasan"
git config --global user.email demo@gmail.com
```

### Working Flow

``` md
( git init ) -Working directory - (git add .) Stagging area - (git commit -m) local repo - (git push) remte repo
```

### tracking 

```md
git status
git diff
```
### commit history

```md
git log
git log --oneline
```

### branching & merging

```md
git branch (working branch check)
git branch branch_name (branch create)
git checkout branch_name (switch branch)
git checkout -b branch_name (create and switch)
```

### Merging

```md
<!-- **two way merge** -->

<!-- first you have to go main or master branch -->
<!-- second this command -->
git merge branch name  <!-- which branch you want to merging with main or master branch-->
```
### Undo Only git-commit or stage
```md
git reset HEAD . (Staging area -> working directory) old -> git restore --staged . (modern)

git reset --soft HEAD~1 (from commit ->Staging area )

git reset --mixed HEAD~1 (from commit ->working directory)
```

### Undo With Code

```md
git checkout . (working directory) old -> git restore . (modern) 

⚠️ Warning: git checkout . বা git restore . দিলে আপনার সব আনসেভড কোড চিরতরে মুছে যাবে!


git reset --hard HEAD (Staging & Working directory)

⚠️ Warning: git reset --hard HEAD দিলে আপনার সাম্প্রতিক সব আনসেভড বা মডিফাইড কোড চিরতরে মুছে যাবে এবং প্রজেক্ট একদম শেষ কমিটের (Last Commit) অবস্থায় চলে যাবে!

```

### To change only the commit message:
```md
git commit --amend -m "new correct commit message"
```

### Modify Last Commit with new add (`--amend`)
```md
1. `git commit -m "first"` (কমিট করলেন)
2. ফাইল চেঞ্জ করে -> `git add .` (ফাইল আপডেট করলেন)
3. `git commit --amend -m "new message"` (আগের কমিটের সাথেই নতুন ফাইল ও মেসেজ একসাথে সেভ হয়ে গেল)
```
### After Push Some Code in Github Modify Last Commit `--amend`

> আমি ভুল করে কিছু file `git add` না করেই GitHub-এ push করে দিয়েছি। এখন বাদ পড়া fileগুলো এবং নতুন code—সবকিছু আগের **একই commit-এর মধ্যে** রাখতে চাই।

```md
1. `git commit -m "first"` (প্রথমে commit করলাম)

2. ফাইল চেঞ্জ করে → `git add .` (নতুন ও বাদ পড়া fileগুলো stage করলাম)

3. `git commit --amend -m "new message"` (আগের commit-এর সাথে নতুন file ও code যোগ করে commit message-ও update করলাম)

4. `git push origin main` (GitHub-এ push করলাম)

5. যদি `non-fast-forward` error আসে → `git push origin main --force` (amend করা commit-টি GitHub-এ update করলাম)
```

### Toggle Previous Branch
- **Description:** আপনাকে হুবহু আগের ব্র্যাঞ্চে (Previous Branch) ফিরিয়ে নিয়ে যায় (ঠিক কম্পিউটারের `Alt + Tab` এর মতো কাজ করে)। বারবার বড় ব্র্যাঞ্চের নাম টাইপ করার ঝামেলা এড়াতে এটি দারুণ একটি শর্টকাট।
```md
git checkout - (old) -> git switch - (modern)
```
### Fast Add & Commit Together

```md
git commit -am "your message"
```
### Correcting commit

```md
git commit --amend (correcting the commit message & added some file in this commit)
- then I for insert something
- then ESE 
- then :wq
```



### .gitignore

```md
Stagging area তে যাবার আগে gitignore এ file or folder add করতে হবে

like before git add . command have to add all file or folder in .gitignore file

```


## Unstagging file 

```md
git add . command দেওয়ার পর যদি মনে পড়ে  কোন file বা folder .gitignore এ add করতে হবে তবে ওই file unstage করে নিতে হবে fist এ

git rm --cached fileName

```

## Main branch থেকে feature branch-এ কোড আনা এবং Push করার নিয়ম

```md
git checkout problem-page
git pull origin main

git checkout main
git pull

git checkout problem-page
git push origin problem-page

```
### Delete a branch
```md
git branch -d Branch_name
```

# Fork & Upstream

যখন অন্য কারো GitHub repository **fork** করে নিজের GitHub-এ নিয়ে কাজ করি, তখন সাধারণত ২টা remote থাকে:

```md
origin   → আমার নিজের fork
upstream → Original repository
```

Example:

```md
Original repository:
https://github.com/mehedihasansufi/documentation

My fork:
https://github.com/Mehedihasan205324/documentation-mehedisufi
```

তখন:

```md
origin   → Mehedihasan205324/documentation-mehedisufi
upstream → mehedihasansufi/documentation
```

### Add Upstream

```md
git remote add upstream https://github.com/ORIGINAL-OWNER/REPOSITORY.git
```

এখানে:

```md
ORIGINAL-OWNER → Original repository owner's GitHub username
REPOSITORY     → Original repository name
```

Example:

```md
git remote add upstream https://github.com/mehedihasansufi/documentation.git
```

### Check Remote

```md
git remote -v
```

এটি local repository-এর সাথে connected সব remote এবং তাদের URL দেখায়।

Example:

origin    → আমার fork
upstream  → original repository

```md
origin    https://github.com/Mehedihasan205324/documentation-mehedisufi (fetch)
origin    https://github.com/Mehedihasan205324/documentation-mehedisufi (push)

upstream  https://github.com/mehedihasansufi/documentation (fetch)
upstream  https://github.com/mehedihasansufi/documentation (push)
```

### Change Upstream URL

যদি `upstream` আগে থেকেই থাকে কিন্তু URL ভুল হয়:

```md
git remote set-url upstream NEW_URL
```

Example:

```md
git remote set-url upstream https://github.com/mehedihasansufi/documentation.git
```

### Fetch Original Repository

Original repository-এর নতুন branch/change-এর information local repository-তে আনতে:

```md
git fetch upstream
```

`fetch` করলে original repository-এর changes **সরাসরি তোমার working directory-তে আসে না**।

এটি শুধু original repository-এর নতুন information/branch local Git-এ update করে।

### Check Upstream Branches

```md
git branch -a
```

এখানে `remotes/upstream/...` দিয়ে original repository-এর remote branches দেখা যাবে।

Example:

```md
remotes/origin/main
remotes/origin/feature/my-task

remotes/upstream/main
remotes/upstream/feature/another-task
```

### Get Original Main Branch Changes

Original repository-এর `main` branch-এর changes নিজের current branch-এ আনতে:

```md
git merge upstream/main
```

অথবা আগে fetch:

```md
git fetch upstream
git merge upstream/main
```

### Push to My Fork

নিজের changes নিজের fork-এ push করতে:

```md
git push origin main
```

অথবা feature branch:

```md
git push origin branch_name
```

## ⚠️⚠️⚠️⚠️ Important

```md
origin   = আমার fork → এখানে সাধারণত আমি push করি

upstream = original repo → এখান থেকে সাধারণত আমি fetch করি
```

### Fork workflow:

```md
Original Repository
        ↓
     upstream
        ↓
    Local Repo
        ↓
      origin
        ↓
     My Fork
```

### Important Commands

```md
git remote -v
```

→ কোন remote কোথায় connected তা দেখায়।

```md
git remote add upstream URL
```

→ নতুন `upstream` remote তৈরি করে।

```md
git remote set-url upstream URL
```

→ existing `upstream`-এর URL পরিবর্তন করে।

```md
git fetch upstream
```

→ original repository-এর নতুন changes/branches-এর information আনে।

```md
git merge upstream/main
```

→ original repository-এর `main` branch-এর changes current branch-এর সাথে merge করে।
