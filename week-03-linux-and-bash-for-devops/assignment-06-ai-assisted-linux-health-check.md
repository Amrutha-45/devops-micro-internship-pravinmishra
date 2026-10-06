# Assignment 6 — Build an AI-Assisted Linux Health Check (AI-Assisted Linux Incident Triage)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build a read-only Bash triage script that checks the health of your Ubuntu server and Nginx application, connect it to Claude Code as a reusable `/linux-triage` skill, simulate a controlled Nginx incident, use the skill to gather and analyze evidence, recover the service manually, and verify recovery. The workflow follows the Agentic Loop: Gather → Analyze → Human Act → Verify.

---

# Task 1 — Confirm the Healthy Baseline and Create the Workspace

## Goal

Confirm that Nginx and the React application are healthy before building the automation.

### Evidence

#### Screenshot 1 — Output of `systemctl is-active nginx`, `ss -ltn | grep ':80'`, and `curl -I http://localhost`

<img width="737" height="347" alt="Screenshot 2026-10-05 210945" src="https://github.com/user-attachments/assets/e99ab5fc-38d8-4170-bb10-26ff4b48eb70" />



#### Screenshot 2 — Output of `pwd` and `find . -maxdepth 4 -type d | sort` showing the workspace folder structure

<img width="912" height="205" alt="Screenshot 2026-10-05 212327" src="https://github.com/user-attachments/assets/979698b1-e75c-4d56-a7a5-cb9a00ecb51d" />


### Notes

Answer the following in your own words:

**1. What proves that Nginx is running?**

The command systemctl is-active nginx returned active, which proves that the Nginx service is currently running.

**2. What proves that the server is listening for HTTP traffic?**

The command ss -ltn | grep ':80' showed that Nginx is listening on port 80, which is the HTTP port.

**3. Why must you capture a healthy baseline before simulating an incident?**

A healthy baseline gives us a reference point. After simulating an incident, we can compare the new results with the baseline to identify what changed and confirm whether the problem was fixed.

# Task 2 — Create Project Context and Safety Rules in CLAUDE.md

## Goal

Tell Claude exactly what this project does and what it is not allowed to do.

### Evidence

#### Screenshot 3 — CLAUDE.md open in VS Code showing all four sections (Project Overview, Incident Workflow, Safety Rules, Output Rules)

<img width="1920" height="1080" alt="Screenshot (205)" src="https://github.com/user-attachments/assets/485c9aa4-8021-4468-8998-37fc57b83b4e" />


### Notes

Answer the following in your own words:

**1. Why should Claude receive project-specific operational rules?**

Claude needs project-specific rules so it understands what the project does, follows the correct incident workflow, and knows which actions are allowed or not allowed during troubleshooting.

**2. Why is the human required to execute the recovery command?**

The workflow focuses on observation and diagnosis first. Claude should recommend the safest recovery action, while changes such as restarting or stopping services should only happen when recovery is explicitly required.

**3. Which rule prevents Claude from making an unsupported diagnosis?**

The Output Rules require Claude to state the likely root cause only when there is enough evidence and include the evidence used to support the diagnosis.

# Task 3 — Use Agentic AI to Plan Before Writing the Script

## Goal

Use Claude Code to inspect the environment and produce a read-only plan before creating any Bash code.

### Evidence

#### Screenshot 4 — Claude Code showing the five-check plan and read-only inspection results

<img width="1536" height="1024" alt="W3A6SS4" src="https://github.com/user-attachments/assets/fad2f70b-a186-4924-99ef-493bba43609a" />


### Notes

Answer the following in your own words:

**1. Which part of this task represents the Gather phase?**

The read-only inspection of the Linux and Nginx environment represents the Gather phase. It collects information about Nginx service health, port 80, HTTP response, disk usage, and memory usage before making any changes.

**2. Did Claude follow the instruction not to create files? How did you verify this?**

Yes. Claude followed the instruction. It performed only read-only inspection commands and did not create, edit, or delete any files. This was verified from Claude's output stating “No files were modified” and from the inspection results showing that only system and Nginx information was collected.

**3. Why is planning before coding useful in DevOps automation?**

Planning before coding helps define the required checks, commands, and safety boundaries before making changes. It reduces mistakes, keeps the automation focused, and ensures that the script follows a safe, read-only diagnostic workflow.

# Task 4 — Build the Linux Triage Bash Script

## Goal

Create one Bash script that gathers consistent Linux and Nginx health evidence.

### Evidence

#### Screenshot 5 — Top section of `linux-triage.sh` showing variables, thresholds, and the checks array

<img width="768" height="387" alt="Screenshot 2026-10-06 065547" src="https://github.com/user-attachments/assets/a3d37a0d-0d4f-4a4d-a46b-b3fc69bee0ae" />


#### Screenshot 6 — Middle section showing check functions and conditionals

<img width="897" height="963" alt="Screenshot 2026-10-06 065919" src="https://github.com/user-attachments/assets/187c10d8-7414-45de-8c48-65a49f7f107f" />


#### Screenshot 7 — Bottom section showing the loop, summary function, and exit behavior

<img width="857" height="966" alt="Screenshot 2026-10-06 070300" src="https://github.com/user-attachments/assets/a5c75e03-0088-4b9d-9b0a-6b5937e2c2e7" />


#### Screenshot 8 — Output of `bash -n scripts/linux-triage.sh` (no syntax errors) and `ls -l scripts/linux-triage.sh` showing executable permission

<img width="820" height="108" alt="Screenshot 2026-10-06 070516" src="https://github.com/user-attachments/assets/c2df4b8f-c34e-414b-a409-168cdde7c215" />


### Notes

Answer the following in your own words:

**1. What is stored in the checks array?**

The checks array stores the names of the five health-check functions:
nginx_service, port_80, http_response, disk_usage, and memory_usage.

**2. How does the `for` loop use that array?**

The for loop goes through each item in the checks array one by one. The case statement then matches each item to its corresponding health-check function and runs it.

**3. Why are the health checks separated into functions?**

Separating the checks into functions makes the script organized, reusable, and easier to maintain. Each function handles one specific health check.

**4. What is the purpose of `$(...)` in this script?**

$(...) is command substitution. It runs a command and stores its output so it can be used as a value in the script. For example, the HTTP status returned by curl is stored in a variable.

**5. Why does the script use different exit codes for HEALTHY, WARN, and FAIL?**

Different exit codes allow other scripts or automation tools to understand the health status of the system. They can distinguish between a healthy result, a warning condition, and a failure and respond accordingly

# Task 5 — Run and Understand the Healthy-State Report

## Goal

Run the Bash script against the healthy server and verify that it creates a report.

### Evidence

#### Screenshot 9 — Output of `./scripts/linux-triage.sh` showing your Full Name and all five check results

<img width="720" height="237" alt="Screenshot 2026-10-06 070903" src="https://github.com/user-attachments/assets/a8919ad8-6915-4c53-ae93-e523e28ea5e4" />


#### Screenshot 10 — Output showing the captured exit code and final summary

S<img width="695" height="262" alt="Screenshot 2026-10-06 071552" src="https://github.com/user-attachments/assets/7f8e542e-ddbb-4ce6-8fdc-e253c67d655b" />



### Notes

Answer the following in your own words:

**1. What is the overall status of your healthy baseline?**

The healthy baseline is HEALTHY. Nginx is active, port 80 is listening, localhost returns an HTTP 200 response, disk usage is low, and sufficient memory is available

**2. Which exact Linux evidence proves the application is serving traffic?**

The strongest evidence is:
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)

from:
curl -I http://localhost

This proves that Nginx is responding successfully to HTTP requests.

**3. Did your script return exit code 0 or 1? Explain why.**

For the healthy baseline, the script returned exit code 0 because all the health checks completed successfully and no failure was detected.

**4. What is the difference between a warning and a failure in this script?**

A warning indicates that a resource is approaching its configured threshold but the service may still be functioning. A failure indicates that an important health check has failed, such as Nginx being inactive or the HTTP response not being successful.

# Task 6 — Create and Run the /linux-triage Skill

## Goal

Turn the Bash script into a reusable, manually invoked Agentic AI workflow.

### Evidence

#### Screenshot 11 — `SKILL.md` showing the frontmatter, allowed tool restrictions, and safety rules

<img width="863" height="742" alt="Screenshot 2026-10-06 071741" src="https://github.com/user-attachments/assets/211b22ec-5589-4828-b001-c2272bd4310c" />


#### Screenshot 12 — `/linux-triage` output for the healthy server

<img width="1312" height="1199" alt="W3A6SS12" src="https://github.com/user-attachments/assets/fcd212ea-6593-4879-ac6e-efbeed3c592c" />


### Notes

Answer the following in your own words:

**1. Why does this skill have Bash, Read, and Grep, but not Write?**

The skill is designed for read-only investigation. Bash is used to run health-check commands, while Read and Grep can inspect existing files and search for relevant information. Write is not included because the skill should not modify files during diagnosis.

**2. Why is `disable-model-invocation: true` useful for this skill?**

It prevents Claude from automatically invoking the skill on its own. The skill runs only when the user explicitly requests it, giving the user more control over when the diagnostic workflow is performed.

**3. What part is performed by Bash, and what part is performed by Claude?**

Bash performs the actual Linux health checks and collects evidence from the system. Claude interprets the collected evidence, identifies patterns or possible problems, and explains the overall health status.

**4. Why is this better than asking Claude "Is my server healthy?" without giving it evidence?**

It is better because Claude receives actual system evidence instead of guessing. The Bash checks provide measurable information about Nginx, port 80, HTTP response, disk usage, and memory, allowing Claude to make a more reliable diagnosis.

# Task 7 — Simulate an Nginx Incident and Let the Skill Diagnose It

## Goal

Create a controlled service failure, gather evidence through Bash, and let Claude analyze the evidence without taking recovery action.

### Evidence

#### Screenshot 13 — Output showing Nginx is inactive and the HTTP request fails

<img width="830" height="142" alt="Screenshot 2026-10-06 072545" src="https://github.com/user-attachments/assets/75513a67-e3b7-46c9-bc69-ddd7677fbb9b" />


#### Screenshot 14 — `/linux-triage` output showing failed evidence, most likely cause, and a suggested recovery command

<img width="1312" height="1199" alt="W3A6SS14" src="https://github.com/user-attachments/assets/333423b4-cd1b-4253-a941-c8b0745139b9" />


#### Screenshot 15 — `incident-failure-report.txt` showing the failed checks and your Full Name

<img width="837" height="550" alt="Screenshot 2026-10-06 074044" src="https://github.com/user-attachments/assets/6fe73ca8-d130-474f-aea0-b881a9c3d23b" />


### Notes

Answer the following in your own words:

**1. Which three checks failed?**

The three failed checks were:
- Nginx service — Nginx was inactive.
- Port 80 — Port 80 was not listening.
- HTTP response — The HTTP request to http://localhost failed.

**2. What evidence supports the conclusion that Nginx is unavailable?**

The evidence was:
- systemctl is-active nginx showed inactive.
- Port 80 was not listening.
- curl -I http://localhost failed to connect.
Together, these results show that Nginx was unavailable.

**3. Did Claude execute the recovery command? Why is that important?**

No. Claude only suggested the recovery command:
sudo systemctl start nginx

It did not execute it. This is important because the triage process should diagnose and explain the incident before making changes, keeping recovery under human control.

**4. Which phase of the Agentic Loop is represented by the Bash report?**

The Bash report represents the Observe / Gather Evidence phase because it collects the actual system health information and failed-check results.

**5. Which phase is represented by Claude's explanation?**

Claude's explanation represents the Reason / Analyze phase because it interprets the collected evidence, identifies the most likely cause, and suggests a recovery action.

# Task 8 — Recover Manually, Verify Again, and Write the Incident Summary

## Goal

Recover the service as the human operator and prove that the system is healthy again.

### Evidence

#### Screenshot 16 — Output showing Nginx is active and `curl -I http://localhost` returns 200 OK

<img width="732" height="237" alt="Screenshot 2026-10-06 074551" src="https://github.com/user-attachments/assets/a7723b6c-3795-4029-a737-5237409640e0" />


#### Screenshot 17 — Second `/linux-triage` output showing successful recovery with no FAIL results

<img width="1448" height="1086" alt="W3A6SS16" src="https://github.com/user-attachments/assets/0ce41532-7d58-472c-8276-618dc40117bd" />


#### Screenshot 18 — Output of `ls -lah reports` showing both `incident-failure-report.txt` and `recovery-report.txt`

<img width="778" height="141" alt="Screenshot 2026-10-06 075609" src="https://github.com/user-attachments/assets/a2e6dc13-29a7-442d-bf12-2225c11ab4b6" />


#### Screenshot 19 — `incident-summary.md` showing all required sections and your Full Name

<img width="816" height="911" alt="Screenshot 2026-10-06 081135" src="https://github.com/user-attachments/assets/471a7e2d-b73a-4ddc-8eb1-ea217eebe2ce" />


### Notes

Answer the following in your own words:

**1. What action did you execute manually?**

I manually executed the recovery command:
sudo systemctl start nginx

**2. What evidence proves that the service recovered?**

The evidence is that Nginx became active, port 80 was listening, and curl -I http://localhost returned HTTP/1.1 200 OK.

**3. Why is the second triage run necessary?**

The second triage run is necessary to verify that the recovery action actually fixed the incident and that all health checks are passing again.

**4. What could go wrong if an AI agent automatically restarted every failed service?**

It could restart a service unnecessarily, interrupt active users or applications, hide the real problem, or cause further system issues without human approval.

**5. In one sentence, explain the difference between using AI as a chatbot and using AI in this agentic workflow.**

A chatbot mainly provides answers, while an agentic workflow uses AI to observe evidence, reason about the problem, plan an action, and verify the result.

# Incident Summary

Fill in all seven sections below in your own words.

**Full Name:** Amrutha Bandi

**Date:** 06/10/2026

---

**1. Reported Symptom**

The Nginx service became unavailable, causing the local website to stop responding to HTTP requests.

**2. Evidence Collected**

The triage checks showed that Nginx was inactive, port 80 was not listening, and curl -I http://localhost failed to connect. Disk and memory usage remained within acceptable limits.

**3. Most Likely Cause**

The most likely cause was that the Nginx service had been stopped, which caused port 80 to stop listening and the local HTTP request to fail.

**4. Human-Approved Recovery Action**

After the failure was diagnosed, I manually executed:
sudo systemctl start nginx

**5. Verification**

After recovery, Nginx was active, port 80 was listening, and curl -I http://localhost returned HTTP/1.1 200 OK. A second triage run confirmed that the health checks passed.

**6. Safety Decision**

The AI was used for observation, analysis, and suggesting the recovery action. The recovery command was executed manually so that the human remained in control of the system-changing action.

**7. Agentic Loop Mapping**

Observe → Bash triage collected system health evidence.
Reason → Claude analyzed the failed checks and identified the likely cause.
Plan → Claude suggested sudo systemctl start nginx.
Act → I manually executed the recovery command.
Verify → Nginx, port 80, HTTP, disk, and memory were checked again to confirm recovery.

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://www.linkedin.com/feed/update/urn:li:activity:7513253173256552448/

#### Screenshot — Published LinkedIn post

<img width="1920" height="1080" alt="Screenshot (206)" src="https://github.com/user-attachments/assets/fd283b79-8ae1-40ef-81a4-7e1014f5b436" />


# GitHub Repository URL

Paste the URL of your GitHub folder or repository containing the assignment files here:

https://github.com/Amrutha-45/devops-micro-internship-pravinmishra/tree/main/dmi-week3-assignment6

# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots and the Bash report
- All written answers must be in your own words
- Do not expose sensitive information (keys, passwords, AWS account IDs, tokens)
- GitHub URL must be included in this document

---

# Completion Checklist

- [ ] Task 1: Healthy baseline confirmed, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: CLAUDE.md created with all four sections (Screenshot 3, Notes answered)
- [ ] Task 3: Five-check plan produced by Claude using read-only tools (Screenshot 4, Notes answered)
- [ ] Task 4: `linux-triage.sh` created, syntax validated, executable permission set (Screenshots 5–8, Notes answered)
- [ ] Task 5: Healthy-state report generated with no FAIL result (Screenshots 9–10, Notes answered)
- [ ] Task 6: `/linux-triage` skill created and run successfully on healthy server (Screenshots 11–12, Notes answered)
- [ ] Task 7: Nginx incident simulated, failed evidence captured, Claude did not execute recovery (Screenshots 13–15, Notes answered)
- [ ] Task 8: Nginx recovered manually, recovery verified, reports saved, incident summary complete (Screenshots 16–19, Notes answered)
- [ ] Incident summary contains all seven required sections
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots and the Bash report
- [ ] Skill does not have Write permission
- [ ] Skill did not execute any recovery commands
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
