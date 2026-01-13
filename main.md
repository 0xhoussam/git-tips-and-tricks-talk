---
title: "Git Workshop: From Zero to Hero"
author: Houssam
---

# Git: Your Code's Time Machine 🕰️
### Phase 1: The Mental Model

---

## The "Old Way" of Saving
We've all been there:

* `final_project.py`
* `final_project_v2.py`
* `final_project_v2_FINAL.py`
* `final_project_v2_FINAL_REAL.py`

<!-- pause -->

**The Problem:** - Which one is actually the latest? 
- How do we go back if we broke something?
- How do we work with others?

<!-- pause -->

## What is Git?
Git is a **Distributed Version Control System**.

* **Version Control:** It tracks every single change to your files.
* **Distributed:** Everyone has a full copy of the project history.

> "Git allows you to take 'snapshots' of your project. If things go wrong, you can teleport back to any snapshot."


<!-- end_slide -->


## The Git Lifecycle (The Most Important Slide)
To use Git, you must understand the **Three States**:

1. **Working Directory:** Where you are currently editing files.
2. **Staging Area:** The "waiting room" where you pick which changes to save.
3. **Local Repository:** The permanent history on your computer.

<!-- pause -->

## The "Big Four" Commands
This is 90% of what you will do every day:

| Command | Action |
| :--- | :--- |
| `git add` | Move changes to the **Staging Area**. |
| `git commit` | Save the snapshot to the **Local Repo**. |
| `git push` | Send your snapshots to **GitHub/Cloud**. |
| `git pull` | Get the latest snapshots from the **Cloud**. |

<!-- end_slide -->

## The "Shopping Trip" Analogy
If Git was a trip to the grocery store, it would look like this:

<!-- pause -->

### 1. The Aisles (Working Directory)
You are walking around, picking up items, and putting them back. 
You’re "editing" what you might want to buy.

<!-- pause -->

### 2. The Cart (Staging Area)
You put specific items into your cart. 
* They aren't "bought" yet. 
* You can still take them out if you change your mind.
* **Command:** `git add <file>`

<!-- pause -->

### 3. The Checkout (Local Repository)
You go to the register and pay. 
* You get a **Receipt** (this is your **Commit**).
* The receipt is a permanent record of exactly what you bought and when.
* **Command:** `git commit -m "Weekly groceries"`


<!-- end_slide -->

# Phase 2: Building Your First Store
## 1. Create the Project

<!-- pause -->

First, we need a folder. Think of this as renting the space for your grocery store.

```bash
mkdir my_grocery_store
cd my_grocery_store
git init
```

<!-- pause -->

Always run this when you are confused.
## 2. The "What's in my cart?" Command
```bash
git status
```
Output: "nothing to commit" (The store is empty!)

<!-- end_slide -->

## 3. Creating our first "Item"
Let's add some milk to our "Aisle."
```bash
echo "1x Carton of Milk" > fridge.txt
git status
```
**Observation**: The file is RED. It’s on the shelf, but not in our cart yet!

<!-- pause -->

## 4. Put it in the Cart (Add)
Let's "Stage" the milk.
```bash
git add fridge.txt
git status
```
**Observation**: The file is GREEN. It’s in the cart!

<!-- end_slide -->

## 5. Checkout (Commit)
Let's lock in the purchase and get our receipt.
```bash
git commit -m "Add milk to the fridge"
```
Pro Tip: The -m is your "Receipt Note." Make it descriptive!

## 6. Reviewing the Receipts
How do we see our history?
```bash
git log
```
Congratulations!
You just created your first "Save Point" in history.


<!-- end_slide -->


## 7. Summary Checklist

- `git init` -> Big Bang.
- `git status` -> See what's happening.
- `git add` -> Put changes in the cart.
- `git commit` -> Get the receipt.


<!-- end_slide -->


# Phase 3: The Safety Net 🪂
### How to fix mistakes and explore "Parallel Universes"

<!-- pause -->

## 1. The "Oops" Button (Undoing)
Imagine you accidentally deleted everything in your file. 
As long as you haven't committed, Git can teleport the file back from your last "Receipt."

```bash
# Let's ruin our file
echo "THIS IS A MISTAKE" > fridge.txt
git status
```

<!-- pause -->
```bash
git restore fridge.txt
cat fridge.txt
```
Result: Your "Milk" is back! Git restored it from the last snapshot.


<!-- end_slide -->


## 2. Branching: Parallel Universes
What if you want to try a crazy new idea (like adding "Chocolate Milk") but you don't want to mess up the original fridge?

<!-- pause -->

**A Branch** is a separate timeline. You can do anything there, and the main timeline stays perfectly safe.

## 3. Creating a New Universe
Let's create a branch called experimental-flavors.

```bash
git switch -c experimental-flavors
# or
git checkout -b experimental-flavors
```
Now let's add something "dangerous":

<!-- pause -->

```bash
echo "1x Chocolate Milk" >> fridge.txt
git add fridge.txt
git commit -m "Testing chocolate milk"
```


<!-- end_slide -->


## 4. Teleporting Between Timelines
Now, watch the magic. Let's go back to the main timeline.

```bash
git switch main
# or 
git checkout main
cat fridge.txt
```
Wait! Where is the Chocolate Milk? It's gone! It only exists in the experimental-flavors universe. Your main fridge is still exactly how you left it.


<!-- end_slide -->


# Phase 3.5: The Merge Conflict 💥
### What happens when two timelines disagree?

## 1. What is a Conflict?
Imagine two people try to change the **exact same line** of the **exact same file** in two different ways.

Git is smart, but it's not a mind reader. It stops and asks: 
> "I don't know which one you want. You decide."

<!-- pause -->

## 2. Setting the Trap
Let's change the milk on our `main` branch.
```bash
# We are on main
echo "1x Organic Whole Milk" >> fridge.txt
git add fridge.txt
git commit -m "Update milk to organic on main"
```

<!-- pause -->

Now, let's go to our other branch and change that same line to something else.
```bash
git switch experimental-flavors
echo "1x Almond Milk" >> fridge.txt
git add fridge.txt
git commit -m "Change milk to almond on branch"
```


<!-- end_slide -->


## 3. The "Explosion"
Now, let's try to bring that experimental-flavors change into main.
```bash
git switch main
git merge experimental-flavors
```

<!-- pause -->

OH NO! Git says: CONFLICT (content): Merge conflict in fridge.txt. The merge has failed. Let's see what the file looks like now.

<!-- pause -->

```bash
cat fridge.txt
```

<!-- end_slide -->

## 4. Reading the "Conflict Markers"
Git has rewritten your file to show you the choices:

```bash
<<<<<<< HEAD
1x Organic Whole Milk  (This is what Main has)
=======
1x Almond Milk         (This is what the Branch has)
>>>>>>> experimental-flavors
```

<!-- pause -->
```bash
git add fridge.txt
git commit -m "Fixed conflict"
```
**Conflict Resolved!**
You are now a Git Master. You faced the "scariest" part of Git and won.


<!-- end_slide -->


# Phase 4: Collaboration
### Taking your code to the Cloud
## Git vs. GitHub
Think of the difference between a file on your Desktop and a Google Doc.

<!-- pause  -->

* **Git:** Like a **Microsoft Word** file on your hard drive. 
  - You can edit it offline.
  - You save versions like `v1`, `v2`.
  - No one else can see it until you send it.

<!-- pause  -->

* **GitHub:** Like **Google Docs**. 
  - It lives on the internet.
  - It is the "Master Copy" that everyone looks at.
  - It lets multiple people suggest changes.


<!-- end_slide -->


## 1. Connecting to the "Server"
To upload your saves, you need to tell your Console where the Cloud Server is.

```sh
# We give the server a nickname: "origin"
git remote add origin https://github.com/user/example.git
```
Origin: This is just a nickname for your GitHub URL so you don't have to type the whole link every time.

<!-- pause -->

## 2. The "Upload" (Pushing)
Think of this as "Uploading" your history.
```sh
git push origin main
```

<!-- pause -->

## 3. The Other Side: Cloning
What if you want to work on a friend's project? You don't init, you clone.
```sh
git clone https://github.com/user/example.git
```
**Note**: Cloning downloads the entire history, every commit, and every branch. It’s a complete copy.


<!-- end_slide -->


## 4. Pulling: Staying in Sync
If your teammate pushes a new feature, your local computer is now "out of date." You need to bring those changes down.
```sh
git pull origin main
```

<!-- pause -->

## 5. The Collaboration Cycle

This is the daily rhythm of a developer:

- git pull (See what others did)
- Work (Change files)
- git add (Put in cart)
- git commit (Get receipt)
- git push (Share with the world)


<!-- end_slide -->


# Phase 5: The Time Traveler's Toolkit

## 1. The "I Forgot Something" Command
Have you ever committed, then realized you forgot to add a file? 
Or worse... you had a typo in your commit message?

> **Don't make a second commit!** Just fix the last one.

<!-- pause -->

### The Scenario:
```bash
echo "1x Eggs" > grocery_list.txt
git add grocery_list.txt
git commit -m "Add egss"
```

<!-- pause -->

Let's fix the "Milk" part:

```sh
echo "1x Milk" >> grocery_list.txt
git add grocery_list.txt
```

<!-- pause -->

Now, let's "rewrite" that last commit:

```bash
git commit --amend -m "Add eggs and milk"
```

<!-- pause -->

**result**:
```sh
git log
```

<!-- end_slide -->


⚠️ The Golden Rule of Amending
Amending is amazing, but it has one big rule:
Never amend a commit that you have already **PUSHED** to GitHub.

<!-- pause -->

Why? Because you are technically "deleting" the old commit and creating a new one. If your friends already downloaded the old one, their "History" will no longer match yours, and the universe will explode (or you'll just get a very annoying error).


<!-- end_slide -->


## 2. Ignore Stuff
The "Blindfold" for Git. There are files you never want to save, such as private passwords, huge "junk" folders, or temporary system files.

```sh
# Create the ignore list
echo "secrets.txt" > .gitignore

# Create a "secret" file
echo "MY_PASSWORD_123" > secrets.txt

# See the result
git status
```
Notice: Git sees the .gitignore file, but it completely ignores the existence of secrets.txt. Your passwords stay off the internet!


<!-- end_slide -->


## 3. git diff
The "Magnifying Glass." While git status tells you what files changed, git diff shows you exactly what lines you added or deleted.
```sh
echo "1x Coffee" >> grocery_list.txt

# Inspect the change
git diff
```
<!-- pause -->
**Pro-Tip**: Always run git diff before you git add. It is the ultimate double-check to make sure you aren't committing any "placeholder" code or mistakes.

<!-- pause -->

## 4. git stash
The "Emergency Pocket." Use this when you're in the middle of a mess, but you suddenly need to switch branches to fix a bug.

```sh
# 1. Hide your messy work in a "stash"
git stash --all

# 2. Your workspace is now clean! Switch branches safely.
# (Do your urgent fix...)

# 3. Bring your work back exactly where you left it
git stash pop
```

The Logic: It takes your uncommitted changes and puts them in a temporary storage drawer, leaving your working directory perfectly clean so you can move around.


<!-- end_slide -->

## 5. git reset
**The Rewind Button.** Sometimes you want to completely discard your recent commits and move the "Time Machine" back to a previous point.

<!-- pause -->

### Three ways to reset:
1. **`--soft`**: Keep your changes in the Staging Area (the cart).
2. **`--mixed`**: Keep your changes in the Working Directory (the aisle).
3. **`--hard`**: **DANGER.** Delete the changes forever.

<!-- pause -->

Warning: --hard is one of the few Git commands that can actually delete your work permanently... or can it?


<!-- end_slide -->


## 6. git reflog
The "Safety Net of the Safety Net." Did you just do a git reset --hard by mistake and lose your work? Don't panic.
Git keeps a secret log of every single place your "Head" has been in the last 30–90 days. This is the Reflog.
```sh
# See every move you've ever made
git reflog
```

<!-- pause -->

How to use it to fix a mistake:
1. Find the point in the list before you messed up (e.g., HEAD@{1}).
2. Reset back to that specific moment.
```sh
git reset --hard HEAD@{1}
```

The Lesson: In Git, it is almost impossible to truly lose data as long as you have committed it at least once.


<!-- end_slide -->


# Phase 6: The 1KRC Challenge
### One Thousand Row Challenge (Collaborative Edition)

## The Scenario
We need to process weather data from a text file. 
* **Student A** builds the "Data Generator."
* **Student B** forks it and builds the "Analytics Engine."

---
<!-- pause -->
## The API Contract 📜
Before you start, both partners must agree on the **Data Format**. 

**File Name:** `weather.txt`
**Format:** `City;Temperature` (Separated by a semicolon)
**Example Line:** `Ben Guerir;28.5`

> **Warning:** No spaces around the semicolon! `City ; Temp` will break the code.

<!-- end_slide -->
## Task 1: The Generator (Student A)
<!-- column_layout: [1, 1] -->
<!-- column: 0 -->
**Goal:** Create the data source.

1. Create GitHub repo: `mini-1brc`.
2. Create `setup_data.py`
3. Crucial: Add weather.txt to your .gitignore before pushing!


<!-- column: 1 -->
## Task 2: The Processor (Student B)
Goal: Parse the strict format and calculate the average.

---
1. Fork and Clone Student A's repo.
2. Create calculate.py.
3. The Logic: You must split the line exactly at the ;.
4. push and open a Pull Request.

<!-- reset_layout -->

## Task 3: Review & Merge (Student A)

Goal: Check the "Contract" and Merge.

1. Open the Pull Request on GitHub.
2. Review: Click "Files Changed." Did Student B use .split(";")?.
3. Merge: Accept the code.
4. Local Sync: Run git pull origin main.


<!-- end_slide -->


# Beyond the Basics: What's Next?
* **`git config`**: Personalize your Git (Themes, Aliases, Default Editor).
* **Git Aliases**: Turn `git commit -m` into just `git cm`.
* **`git worktree`**: Work on two different branches at the exact same time in two different folders. No stashing required!
* **`git rebase`**: "Clean up" your history by moving your commits to the tip of a new branch.
* **`git bisect`**: Use binary search to find exactly which commit introduced a bug.

# Resources

<!-- column_layout: [1, 1] -->
<!-- column: 0 -->
![building-git](./building-git.jpg)
<!-- column: 1 -->
![progit2](./progit2.png)

<!-- end_slide -->


# 🙏 Thank You!

### **Questions?**
### [0xhoussam]
