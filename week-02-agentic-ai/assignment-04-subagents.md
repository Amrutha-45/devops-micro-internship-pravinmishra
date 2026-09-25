# Assignment 4 — Building Your AI Team

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build and configure a set of specialized AI subagents inside your project. You will learn how different models and tool permissions define agent behavior, and you will trigger two real agent delegations to analyze security and cost aspects of your Terraform infrastructure.

---

# Task 1 — Create the Agents Folder and Add Files

## Goal

Create the `.claude/agents/` directory and add all required agent files.

### Evidence

#### Screenshot 1 — VS Code sidebar showing `.claude/agents/` with all 3 files

<img width="1408" height="1005" alt="WEEK2A4SS1" src="https://github.com/user-attachments/assets/8544b92b-2eb7-4397-aab0-c523313f92cb" />



# Task 2 — Compare the Agent Configurations

## Goal

Analyze the configuration differences between the three agents and demonstrate understanding of model and tool selection.

### Written Answers

#### 1. Why does the cost optimizer use Haiku instead of Sonnet?

The cost optimizer uses Haiku because cost analysis is a focused task that does not always require the higher reasoning capability of Sonnet. Haiku provides faster and more economical processing while still being suitable for analyzing infrastructure costs.

#### 2. Why does the security auditor NOT have Write in its tools list?

The security auditor is only meant to inspect and analyze the Terraform infrastructure. It does not have the Write tool so that it cannot accidentally modify project files while performing a security review.

#### 3. Why does the tf-writer use `inherit` instead of a specific model?

The tf-writer uses inherit so that it uses the model configuration from the main Claude Code session instead of being tied to one specific model. This makes the agent more flexible.

### Evidence

#### Screenshot 2 — `security-auditor.md` frontmatter showing model and tools configuration

<img width="1422" height="1013" alt="WEEK2A4SS2" src="https://github.com/user-attachments/assets/59c6674f-c1c3-4b2c-b14b-c891ca6b8276" />


#### Screenshot 3 — `cost-optimizer.md` frontmatter showing the model and tools configuration

<img width="1391" height="1002" alt="WEEK2A4SS3" src="https://github.com/user-attachments/assets/43d91ebd-6137-46f8-a099-561f92e4eee7" />


# Task 3 — Run the Security Auditor

## Goal

Trigger the security auditor agent and analyze the generated security report for your Terraform infrastructure.

### Evidence

#### Screenshot 4 — The delegation message showing Claude launched the security-auditor

<img width="1920" height="1080" alt="WEEK2A4SS4" src="https://github.com/user-attachments/assets/a5f8519b-066d-4058-b138-b732c92cc01d" />


#### Screenshot 5 — Security audit report output

<img width="1347" height="717" alt="WEEK2A4SS5" src="https://github.com/user-attachments/assets/a22e444b-7c3d-4425-904d-ff4099bfa9d9" />


# Task 4 — Run the Cost Optimizer

## Goal

Trigger the cost optimizer agent and review the generated cost optimization report.

### Evidence

#### Screenshot 6 — The full cost optimization report

<img width="1267" height="596" alt="WEEK2A4SS6" src="https://github.com/user-attachments/assets/0106a4eb-4fbe-4c5d-9ee7-7b16781171a5" />


# Submission Instructions

- Ensure all agent files are committed in `.claude/agents/`
- Complete all written answers in your GitHub Repo
- Push final changes to your forked GitHub repository

---

## GitHub Repository URL

Paste your forked repository URL here:

`Add your URL here`

---

# Completion Checklist

- [ ] `.claude/agents/` folder contains all 3 agent files
- [ ] Screenshot 2 shows correct `security-auditor.md` configuration
- [ ] Screenshot 3 shows correct `cost-optimizer.md` configuration
- [ ] All 3 written answers completed 
- [ ] Security auditor executed successfully
- [ ] Cost optimizer executed successfully
- [ ] Security report is visible with findings
- [ ] Cost report is visible with recommendations
- [ ] All required screenshots added
- [ ] GitHub repo updated with agents

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
