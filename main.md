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
