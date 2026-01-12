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
