# Assignment 3 — CodeTrack: Branching Workflow (Add & Verify a Contact Page)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will add a new Contact page to CodeTrack using a clean feature-branch workflow. You will keep each change in a separate commit, prove that your default branch remains unchanged before the merge, and validate the result after merging.

---

# Task 1 — Confirm Repository State and Default Branch

## Goal

Start from a clean default branch (`main` or `master`) and confirm the repository status.

### Evidence

#### Screenshot 1 — Output of `git status` and `git branch` showing a clean status and the default branch checked out

<img width="497" height="140" alt="image" src="https://github.com/user-attachments/assets/329aaf74-1f7c-4681-bc68-af5dab211839" />


# Task 2 — Create and Switch to a Feature Branch

## Goal

Create a branch named exactly `feature/contact-page` and switch to it.

### Evidence

#### Screenshot 2 — Output of `git checkout -b feature/contact-page` and `git branch` showing `* feature/contact-page`

<img width="588" height="168" alt="image" src="https://github.com/user-attachments/assets/cf6f99f1-538f-4569-b03c-508350ff3af0" />


# Task 3 — Add contact.html on the Feature Branch

## Goal

Create `contact.html` with the provided content and commit it alone using the message `feat(contact): add Contact page`.

### Evidence

#### Screenshot 3 — Output of `ls` showing `contact.html`

<img width="442" height="75" alt="image" src="https://github.com/user-attachments/assets/bf75dd93-2978-4a20-bf62-41b073d5df82" />


#### Screenshot 4 — Output of `git commit`

<img width="581" height="167" alt="image" src="https://github.com/user-attachments/assets/c24b48ad-4031-4a08-a042-d1f615091e70" />


#### Screenshot 5 — Output of `git log --oneline -3` showing the new commit

<img width="578" height="171" alt="image" src="https://github.com/user-attachments/assets/43440be1-a15d-4d61-b77e-9e2a1227ba16" />


# Task 4 — Add the Contact Link to index.html

## Goal

Add the provided Contact Page link to `index.html` and commit it separately using the message `feat(nav): add Contact Page link`.

### Evidence

#### Screenshot 6 — Output of `git status` showing `index.html` as modified before staging

<img width="575" height="250" alt="image" src="https://github.com/user-attachments/assets/ff8a4cd8-28f6-406f-83fd-9853a2666fa3" />


#### Screenshot 7 — Output of `git commit`

<img width="581" height="136" alt="image" src="https://github.com/user-attachments/assets/bb5895f2-d381-4f24-97aa-d5d494a7eb91" />


#### Screenshot 8 — Browser showing the Contact Page link on the homepage while on `feature/contact-page`

<img width="1157" height="477" alt="image" src="https://github.com/user-attachments/assets/6ae68cee-b614-461e-a2e8-32c1b7558264" />


# Task 5 — Verify Isolation (Prove the Default Branch Is Unchanged)

## Goal

Switch back to the default branch and confirm that `contact.html` and the Contact Page link do not exist there yet.

### Evidence

#### Screenshot 9 — Terminal showing the checkout and `ls` output, proving `contact.html` is absent

<img width="650" height="201" alt="image" src="https://github.com/user-attachments/assets/f679d0c0-f1d7-4041-9df8-5491bd8f2fd8" />


#### Screenshot 10 — Browser showing the homepage on the default branch with no Contact Page link

<img width="802" height="428" alt="image" src="https://github.com/user-attachments/assets/9730d92a-9f77-41d6-9b9f-516d17941583" />

# Task 6 — Merge the Feature Branch into the Default Branch

## Goal

Merge `feature/contact-page` into your default branch and confirm the Contact page works.

### Evidence

#### Screenshot 11 — Output of `git merge feature/contact-page`

<img width="586" height="242" alt="image" src="https://github.com/user-attachments/assets/e0efb2af-e117-4e92-920e-3f5032215618" />


#### Screenshot 12 — Output of `ls` showing `contact.html` after the merge

<img width="515" height="150" alt="image" src="https://github.com/user-attachments/assets/48bb3902-a7cd-46b5-a4cd-a8ee4aa8cc44" />


#### Screenshot 13 — Browser showing the Contact page opened from the homepage link on the default branch

<img width="820" height="408" alt="image" src="https://github.com/user-attachments/assets/58b5c34a-1a02-4b85-9912-47a95b84666a" />


# Task 7 — Inspect History (Graph View)

## Goal

Display the repository history as a graph and locate both feature commits.

### Evidence

#### Screenshot 14 — Full output of `git log --oneline --graph --decorate --all`

<img width="581" height="233" alt="image" src="https://github.com/user-attachments/assets/c19c2c76-7e00-404f-ba05-2db1ac908a21" />

# Task 8 — Optional Cleanup (Delete the Feature Branch)

## Goal

Delete the merged `feature/contact-page` branch to keep your branch list clean.

### Evidence

#### Screenshot 15 (Optional) — Output showing `feature/contact-page` deleted and no longer listed

<img width="637" height="63" alt="image" src="https://github.com/user-attachments/assets/4f2ab9a6-613f-4694-b5f9-99c31219f5e9" />


# Submission Instructions

- Tasks 1–7 are required; Task 8 is optional
- Add all required screenshots in your submission
- Evidence must show `contact.html` and the homepage link were absent before merging, and working after merging
- Do not expose passwords, access tokens, or private keys

---

# Completion Checklist

- [ ] Repository confirmed clean on the default branch (Screenshot 1)
- [ ] `feature/contact-page` created and checked out (Screenshot 2)
- [ ] `contact.html` added in its own commit (Screenshots 3–5)
- [ ] Homepage Contact link added in a separate commit (Screenshots 6–8)
- [ ] Default branch proven unchanged before merge (Screenshots 9–10)
- [ ] Feature branch merged and Contact page verified (Screenshots 11–13)
- [ ] Graph history reviewed (Screenshot 14)
- [ ] Optional cleanup completed (Screenshot 15)
- [ ] No sensitive data exposed

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
