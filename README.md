# Number Guessing Game - Repository Documentation

## Initial Branch Structure

At the start of the project, the repository contains the following branches:

- **main**: The stable baseline containing the initial Number Guessing Game.
- **dev**: The active development integration branch containing player encouragement messages.
- **feature1**: Implements game controls including quitting with negative input, replay loops, and guess feedback.
- **feature2**: Implements attempt restrictions, tracking max attempts and handling game-over conditions.
- **feature3**: Implements hint functionality across multiple iterative commits.
- **hotfix**: Contains a targeted bugfix ensuring the random integer generator includes the maximum range boundary.

---

## Git Workflow & History Analysis

### 1. Differences Between Integration Strategies

| Strategy | How It Works | What the History Looks Like | When to Use It |
| :--- | :--- | :--- | :--- |
| **`git merge`** | Combines two branches and creates a new merge commit connecting their histories. | Shows parallel branch lines joining back together into the main line. | Merging a completed feature or user story branch into `dev` or `main`. |
| **`git rebase`** | Takes commits from your current branch and replays them on top of another branch. | Keeps history in a straight line instead of showing separate branch paths. | Updating your local feature branch with the latest changes from `dev`. |
| **`git squash`** | Combines multiple commits into a single commit with one message. | Cleans up the log by replacing several small commits with one clean commit. | Packaging your work before sharing it so others don't see small "work-in-progress" commits. |
| **`git cherry-pick`** | Grabs a specific commit from one branch and applies it directly to your current branch. | Adds that single commit to your branch without bringing along any other commits. | Copying an urgent bug fix directly into `main` without merging unfinished features from `dev`. |

---

### 2. History Observations: `feature1` vs. `feature2` vs. `feature3`

* **`feature1` (Standard Merge):**
    * Merged directly into `dev` using `git merge`, which created merge commit `912a1bc`.
    * In the git graph, you can clearly see the line branch off for the feature commit and reconnect to `dev`. It makes it obvious when the branch started and ended, though having too many of these can make the log look cluttered.

* **`feature2` (Updating the Feature Branch First):**
    * We merged `dev` into `feature2` before bringing `feature2` into `dev`. This created merge commit `16dcdc8`.
    * Doing this let us resolve conflicts between the max attempts limit and the new hints locally on `feature2`. It kept `dev` safe and working while we fixed and tested the code.

* **`feature3` (Squash, Rebase, and Fast-Forward):**
    * Originally had four separate commits while working on the hint feature.
    * We squashed them into a single clean commit (`70648b2`) and rebased onto `dev`.
    * Because it was rebased to the tip of `dev`, merging it back was a simple fast-forward. In `git log`, it sits directly in a straight line with no branching lines or extra merge commits.

---

### 3. Real-World Project Applications

* **Rebase:** Keeping your personal feature branch up to date while working locally so you do not fall behind the team's shared `dev` branch.
* **Squash:** Cleaning up small, messy commits (like "fix typo" or "quick test") into one clear commit before submitting a pull request for review.
* **Merge:** Bringing a completed, tested user story into `dev`, leaving a clear record of when that feature was integrated.
* **Cherry-Pick:** Fixing an emergency bug on the production release (`main`) by applying only the bug fix commit without accidentally releasing unfinished work from `dev`.