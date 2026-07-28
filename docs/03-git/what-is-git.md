# What Is Git?

> Git is a distributed version control system that tracks changes to files, enabling collaboration, history inspection, and safe experimentation.

> **Related:** [Basic Workflow](basic-workflow.md) | [Branching & Merging](branching.md)

---

## What Is It?

Git is a tool that records snapshots of your project over time. Every time you commit, Git takes a picture of what your files look like and stores a reference to that snapshot. If files haven't changed, Git links to the previous identical copy rather than duplicating it.

Unlike older version control systems (like SVN or CVS), Git is **distributed** — every developer has a full copy of the entire repository history on their machine. This means you can work offline, experiment freely, and never lose history.

## Why Does It Matter?

Version control is the safety net of software development. It lets you:

- **Experiment without fear** — try a risky refactor and abandon it if it doesn't work
- **Collaborate without conflict** — multiple people can work on the same codebase simultaneously
- **Understand what happened** — see who changed what, when, and why
- **Recover from mistakes** — revert to any point in history

Git is the industry standard. Knowing it is a prerequisite for professional development.

## Key Concepts

| Concept | What It Is |
|---------|------------|
| Repository | A project folder tracked by Git |
| Commit | A snapshot of your files at a point in time |
| Branch | A movable pointer to a commit — a line of development |
| Remote | A copy of the repository hosted elsewhere (e.g., GitHub) |
| Working Tree | The actual files you see and edit |
| Staging Area | A middle ground between your working tree and the next commit |

## What's Next?

Start with the [Basic Workflow](basic-workflow.md) to make your first commit.
