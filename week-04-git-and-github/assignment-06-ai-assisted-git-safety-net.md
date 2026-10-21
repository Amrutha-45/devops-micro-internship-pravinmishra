# Assignment 6 — Building an AI-Assisted Git Safety Net (PR Ready Check)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In Week 2 you built Claude Code hooks that block a dangerous action *before* it happens (`PreToolUse`), and a restricted skill that could look but not touch (`allowed-tools` without `Write`). In this assignment you will discover that Git has the exact same idea, decades older: a **pre-commit hook** that blocks a commit before it's created.

You will build both halves of a real "PR Ready" workflow:

1. A **Git hook that follows fixed rules** — scans staged changes for hardcoded secrets and oversized files and refuses the commit. No AI involved, no guessing, just a rule that gives the same answer every time.
2. A **restricted Claude Code skill** (`/pr-ready`) that reads your staged diff and drafts a Pull Request title, description, and a short list of things worth a second look — the kind of judgment a fixed rule can't make (mixed changes, missing context, unclear intent). The skill never commits, pushes, or opens the PR. You do that yourself, using its draft as a starting point.

This mirrors the Agentic Loop from Week 3's Linux triage assignment: **Gather → Analyze → Human Act → Verify**. The hook and the skill both gather and analyze; only you act.

---

# Task 0 — Confirm Your Fork and Create a Feature Branch

## Goal

Confirm you are working in your own fork, then create a dedicated branch for this assignment.

### Evidence

#### Screenshot 1 — Output of git remote -v and git branch showing the new branch

<img width="621" height="350" alt="image" src="https://github.com/user-attachments/assets/f5176ecb-5e3f-4888-8f88-727fd232e304" />


### Notes

**1. Why create a dedicated branch instead of doing this work on main?**

A dedicated branch keeps my assignment changes separate from the main branch. It allows me to test the pre-commit hook, fix issues, and review my work safely without affecting the main branch.

# Task 1 — Stage a Change With Realistic Risk

## Goal

On your own fork of this repository (the one you've been submitting your DMI work in since onboarding), create a new branch and stage a change that a real reviewer should catch: a hardcoded-looking secret and a leftover debug statement.

### Evidence

#### Screenshot 1 — Output of  `git status` showing the staged file on feature/ai-pr-ready

<img width="535" height="173" alt="image" src="https://github.com/user-attachments/assets/2a2d46ec-fa01-4014-bd19-1be8b48dbb5f" />


### Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

The assignment uses an obviously fake key to safely test whether the pre-commit hook can detect secret-like patterns without exposing real credentials. Using a real key could compromise security and lead to unauthorized access or misuse.

# Task 2 — Write a Real Git Pre-Commit Hook

## Goal

Create a tracked, shareable pre-commit hook that blocks a commit containing secret-like patterns or files over 1MB.

### Evidence

#### Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

<img width="587" height="301" alt="image" src="https://github.com/user-attachments/assets/721b2a5e-5555-46df-b13f-37c42020646d" />


#### Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

<img width="667" height="123" alt="image" src="https://github.com/user-attachments/assets/a2877309-b8fb-4a55-85e4-13c5fb2892a9" />


### Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

Tracking hooks/pre-commit in the repository makes the hook shareable, version-controlled, and available to other contributors. Files in .git/hooks/ are local to one clone and are not included in normal Git commits, so other contributors would not automatically receive the same safety checks.

**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

PreToolUse in Claude Code intercepts a tool call before it executes, allowing dangerous actions to be blocked in advance. A Git pre-commit hook intercepts a commit before it is created and checks staged changes for issues such as secret-like patterns or oversized files. Both act as preventive safety gates that enforce rules before an action happens.

# Task 3 — Prove the Hook Blocks the Risky Commit

## Goal

Attempt to commit the staged file from Task 1 and show the hook rejecting it.

### Evidence

#### Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file

<img width="607" height="172" alt="image" src="https://github.com/user-attachments/assets/35cc7e34-974c-42df-96fd-ba645f8b59ad" />


### Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

The pattern AKIA[0-9A-Z]{16} matched the fake key because it starts with AKIA followed by 16 uppercase letters or digits. The hook recognized this AWS-style access key pattern and blocked the commit.

**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**

The hook might not catch a secret without the AKIA prefix if it doesn't match any of the defined patterns. This shows that fixed rules are consistent and predictable but cannot detect every possible secret format, so additional tools and human review are important.

# Task 4 — Build the `/pr-ready` Skill

## Goal

Create a manually invoked Claude Code skill that reads your staged changes and produces a PR-readiness report and a draft PR description — without writing, committing, or pushing anything itself.

### Evidence

#### Screenshot 5 — `SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no `Write`) and `disable-model-invocation: true`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/de2f652a-44b3-4f07-a744-56bcbab6c472" />


#### Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5b706d9f-1d79-40c4-bbeb-0d4c548db1d0" />


### Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

Bash allows /pr-ready to run read-only Git commands to inspect the repository and staged changes, while Read allows it to examine relevant files. The Write tool is excluded to prevent the skill from modifying or creating files. This keeps the review read-only and ensures that the developer remains in control of all changes.

**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

Both checks identified the fake AWS-style access key and the temporary debug statement. The pre-commit hook used predefined patterns to detect secret-like strings and block the commit, while /pr-ready provided contextual analysis, explaining why the findings were risky and recommending fixes. The hook enforces fixed rules consistently, whereas the AI review can explain concerns and suggest improvements. Neither approach guarantees that every possible security issue will be detected.

# Task 5 — Fix the Issues and Re-Verify

## Goal

Remove the secret and debug statement, then prove both gates now pass clean.

### Evidence

#### Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)

<img width="831" height="173" alt="image" src="https://github.com/user-attachments/assets/38e2bb9a-8629-48cd-8251-f3efd182317c" />


#### Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/980371df-e9c3-42a2-b79e-5ca07d17e7fd" />


### Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

I fixed the trailing whitespace in .claude/skills/pr-ready/SKILL.md and updated hooks/pre-commit so it reports a secret-like pattern without printing the matched content. These changes improve code cleanliness and prevent potential credential disclosure in terminal or CI logs.

# Task 6 — Push and Open a Pull Request Using the AI Draft

## Goal

Push your branch and open a real Pull Request, using `/pr-ready`'s drafted title and description as your starting point — read it critically and edit before you use it.

**Important:** Open this Pull Request with base repository set to **your own fork** — not the shared upstream `pravinmishraaws/devops-micro-internship-pravinmishra` repository. This assignment's hook and skill files are your own practice work, not a change meant for the shared class repo.

### Evidence

#### Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d1e08512-138b-4ca0-a86c-09d7448586e9" />


#### PR Link

https://github.com/Amrutha-45/CodeTrack/pull/1?utm_source=chatgpt.com

### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

I reviewed the AI-generated draft and edited the description to accurately reflect the changes made, the validation performed, and the remaining limitations. I ensured that I did not claim the Claude Code /pr-ready review had succeeded because it was blocked by a credit limitation. This made the PR description more accurate and transparent.

**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

The AI might include incorrect claims, overlook security risks, or state that tests and reviews passed when they were never completed. It could also suggest an unsuitable title or description that misrepresents the changes. Reviewing the draft helps me catch errors and remain responsible for the final PR.

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

This PR contains my practice work for the assignment, including the PR-readiness skill and pre-commit safety hook. Targeting my own fork, Amrutha-45/CodeTrack, keeps these experimental changes separate from the shared upstream repository, pravinmishraaws/devops-micro-internship-pravinmishra, and prevents accidental changes to the class project.

# Task 7 — Map the Workflow to the Agentic Loop

## Goal

Explain this assignment's workflow using the same Gather → Analyze → Human Act → Verify structure from Week 3.

### Notes

**1. Which step(s) represent Gather?**

Gather is the step where I used Git commands to inspect the repository status, staged changes, and branch diff using commands such as git status --short, git diff --cached, and git diff master...HEAD. These commands collected the information needed to review the changes.

**2. Which step(s) represent Analyze?**

Analyze is the step where I used the pre-commit hook and AI-assisted review to identify secret-like patterns, debug statements, whitespace errors, and potential risks. The hook applied fixed rules, while the AI review provided contextual feedback and suggested improvements.

**3. Which step is Human Act, and why must a human — not Claude — run `git commit`, `git push`, and open the PR?**

Human Act is the step where I reviewed the findings, corrected the files, ran the commit, pushed the feature branch, and opened the pull request. A human must control these actions to verify the changes, authorize modifications to the repository, and prevent unintended commits, pushes, or pull requests.

**4. Which step is Verify?**

Verify is the step where I checked the hook's behavior, confirmed that the commit passed the pre-commit checks, reviewed whitespace and Bash syntax, and confirmed that the feature branch was pushed and the pull request was open. Verification helps ensure that the intended changes were applied, although it does not guarantee that every possible security issue has been detected.

**5. In one or two sentences: why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

The pre-commit hook consistently blocks specific issues, such as matching secret-like patterns and oversized staged files, before a commit is created. The AI skill can provide broader contextual analysis and recommendations, so using both offers complementary protection while still requiring human review.

# Task 8 — LinkedIn Post

## Goal

Publish a LinkedIn post summarizing what you built and what you learned about combining fixed-rule safety checks with AI-assisted review.

### Evidence

#### LinkedIn Post URL

https://www.linkedin.com/feed/update/urn:li:share:7518664738201886720/

## Key Learnings

1. Learned how Git pre-commit hooks can prevent commits containing secret-like patterns or oversized staged files.
2. Understood why repository-tracked hooks are easier to share and maintain than local Git hooks.
3. Learned how AI-assisted review can identify potential risks and help draft pull request descriptions.
4. Practiced the Gather → Analyze → Human Act → Verify workflow while keeping important Git operations under human control.
5. Understood that AI reviews and fixed-rule checks have limitations, so code changes must be verified before pushing or merging.



# Submission Instructions

- Ensure `hooks/pre-commit` and `.claude/skills/pr-ready/SKILL.md` are committed to your GitHub repository
- Add all required screenshots to your submission
- All written answers must be in your own words
- Do not use a real secret or credential anywhere in your submission — the fake key in Task 1 is intentional and must stay clearly fake
- Open your Pull Request against your own fork, not the shared upstream repository
- Push your final changes to your forked repository
- Include your PR link and LinkedIn post URL

---

## GitHub Repository URL

Paste your forked repository URL here:

https://github.com/Amrutha-45/CodeTrack

# Completion Checklist

- [ ] Branch `feature/ai-pr-ready` created with a staged file containing a fake secret and a debug statement
- [ ] `hooks/pre-commit` created and tracked in the repo (not only in `.git/hooks/`)
- [ ] `core.hooksPath` configured to point at `hooks/`
- [ ] Pre-commit hook shown blocking the risky commit
- [ ] `.claude/skills/pr-ready/SKILL.md` created with correct `allowed-tools` (no `Write`) and `disable-model-invocation: true`
- [ ] `/pr-ready` run against the risky diff and shown flagging issues
- [ ] Risky file fixed; `git commit` succeeds cleanly
- [ ] `/pr-ready` re-run showing a clean report and drafted PR title/description
- [ ] Pull Request opened using the AI draft as a starting point, with your own fork as the base repository (not upstream), PR link included
- [ ] Agentic Loop mapping (Task 7) completed in your own words
- [ ] LinkedIn post published and URL submitted
- [ ] All required screenshots added
- [ ] GitHub repository URL provided

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
