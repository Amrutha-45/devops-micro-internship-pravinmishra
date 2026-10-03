# Assignment 5 — Bash Script Automation Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will practice Bash scripting by building a series of small automation scripts covering environment setup, variables, arrays, loops, file conditionals, if-else logic, and functions. These scripts form the foundation of real-world Linux automation used in DevOps, cloud, and production support environments.

---

# Task 1 — Bash Environment & Workspace Setup

## Goal

Verify that Bash is available on your system and create a clean workspace for this assignment.

### Evidence

#### Screenshot 1 — Output of `echo $SHELL` and `bash --version`

<img width="753" height="380" alt="W3A5SS1" src="https://github.com/user-attachments/assets/bcb925f8-606c-40af-a0e6-a83d2e1a74be" />


#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

<img width="687" height="161" alt="W3A5SS2" src="https://github.com/user-attachments/assets/383f9d4a-bc3a-44b8-844c-6c77105e1736" />


### Notes

Answer the following in your own words:

**1. What is Bash?**

Bash is a command-line shell used in Linux to run commands and execute scripts. It also provides a scripting language that can be used to automate tasks.

**2. What is the difference between shell and Bash?**

A shell is a program that allows us to interact with the operating system through commands. Bash is one type of shell. Other shells include Zsh and Fish.

**3. Why is it important to confirm the Bash version before writing scripts?**

It is important to check the Bash version because some commands and features may work differently in different versions. Checking the version helps make sure the script will run correctly on the system.

# Task 2 — Your First Bash Script

## Goal

Create your first Bash script, make it executable, and run it from the terminal.

### Evidence

#### Screenshot 1 — Content of `first-script.sh`

<img width="827" height="163" alt="Screenshot 2026-10-03 211817" src="https://github.com/user-attachments/assets/56ee9b14-ec9b-47f2-ac14-ba3338c77572" />


#### Screenshot 2 — Output of `./first-script.sh`

<img width="913" height="133" alt="Screenshot 2026-10-03 212301" src="https://github.com/user-attachments/assets/e250d641-feef-42bb-b9e2-cd6c189188af" />


#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission

<img width="825" height="40" alt="Screenshot 2026-10-03 212417" src="https://github.com/user-attachments/assets/d4feebea-2742-496c-9b8f-033a687e7c0c" />


### Notes

Answer the following in your own words:

**1. What is the purpose of `#!/bin/bash`?**

#!/bin/bash tells the system to use Bash to execute the script.

**2. Why do we use `chmod +x` before running a script?**

chmod +x gives the script permission to be executed. After this, we can run it directly using ./script.sh.

**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**

./script.sh runs the script as an executable and uses the interpreter mentioned in the first line of the script. bash script.sh directly tells Bash to run the script.

# Task 3 — Variables: User Information Script

## Goal

Use variables to store and display user-related information.

### Evidence

#### Screenshot 1 — Content of `user-info.sh`

<img width="890" height="245" alt="Screenshot 2026-10-03 212758" src="https://github.com/user-attachments/assets/0bbdb63a-cccf-4329-bc43-9994225e261c" />


#### Screenshot 2 — Output of `./user-info.sh`

<img width="733" height="98" alt="Screenshot 2026-10-03 212916" src="https://github.com/user-attachments/assets/eb58a66a-2399-415f-a443-f74c2249a262" />


### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

A variable in Bash is a name used to store a value, such as text or a number, so that it can be used later in the script.

**2. Why should we avoid spaces around the `=` sign when creating variables?**

Bash does not allow spaces around = during variable assignment. Spaces can make Bash treat the assignment as a command instead of a variable.

**3. How do you access the value stored inside a Bash variable?**

We use the $ symbol followed by the variable name. For example, if the variable is name, we use $name to access its value.

# Task 4 — Arrays & Loops: Tools Checklist Script

## Goal

Use arrays and loops to print a checklist of tools used in Bash scripting.

### Evidence

#### Screenshot 1 — Content of `tools-checklist.sh`

<img width="787" height="240" alt="Screenshot 2026-10-03 213058" src="https://github.com/user-attachments/assets/6c50af79-441e-48c1-8b86-74e79822f128" />


#### Screenshot 2 — Output of `./tools-checklist.sh`

<img width="796" height="165" alt="Screenshot 2026-10-03 213244" src="https://github.com/user-attachments/assets/0400cdb3-02ad-40f5-bacd-7ba287fcbec5" />


### Notes

Answer the following in your own words:

**1. What is an array in Bash?**

An array in Bash is a variable that can store multiple values under one name.

**2. Why are arrays useful in scripts?**

Arrays are useful for storing related values together and processing them easily using loops.


**3. What does `"${tools[@]}"` mean?**

"${tools[@]}" represents all the values stored in the tools array, with each value treated as a separate item.

**4. What is the purpose of the `for` loop in this script?**

The for loop is used to go through each tool in the array one by one and print it as part of the checklist.

# Task 5 — Loops: Number Counter Script

## Goal

Use loops to repeat a task multiple times.

### Evidence

#### Screenshot 1 — Content of `counter.sh`

<img width="757" height="240" alt="Screenshot 2026-10-03 213531" src="https://github.com/user-attachments/assets/df59c20a-42a7-49f3-8537-74c8cc70ed5a" />


#### Screenshot 2 — Output of `./counter.sh`

<img width="781" height="180" alt="Screenshot 2026-10-03 213645" src="https://github.com/user-attachments/assets/167908c6-e18a-4309-b477-3ced5a368f85" />


### Notes

Answer the following in your own words:

**1. What is a loop?**

A loop is a programming structure that repeats a set of commands multiple times.

**2. Why do we use loops in Bash scripting?**

We use loops to automate repetitive tasks without writing the same commands again and again.

**3. How many times did the loop run in your script?**

The loop ran 5 times.

**4. What would you change if you wanted the loop to run 10 times?**

I would change {1..5} to {1..10} in the for loop.

# Task 6 — Files & Conditionals: File Validation Script

## Goal

Use file checks and conditionals to verify whether files and directories exist.

### Evidence

#### Screenshot 1 — Output of `ls -lah ../test-folder`

Add your screenshot here.

---

#### Screenshot 2 — Content of `file-check.sh`

Add your screenshot here.

---

#### Screenshot 3 — Output of `./file-check.sh`

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What does `-d` check in Bash?**

-d checks whether the given path exists and is a directory.

**2. What does `-f` check in Bash?**

-f checks whether the given path exists and is a regular file.

**3. Why should file and directory paths be stored in variables?**

Storing paths in variables makes the script easier to read, update, and maintain because we can change the path in one place.

**4. What happens if the file does not exist?**

The file check condition becomes false, so the script executes the else block and displays a message saying that the file does not exist.

# Task 7 — Conditionals: Pass or Retry Script

## Goal

Use if-else conditionals to make decisions based on a variable value.

### Evidence

#### Screenshot 1 — Content of `score-check.sh` with `score=85`

Add your screenshot here.

---

#### Screenshot 2 — Output showing `Result: Pass`

Add your screenshot here.

---

#### Screenshot 3 — Content of `score-check.sh` with `score=55`

Add your screenshot here.

---

#### Screenshot 4 — Output showing `Result: Retry`

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What is the purpose of if-else in Bash?**

if-else is used to make decisions in a script based on whether a condition is true or false.

**2. What does `-ge` mean?**

-ge means greater than or equal to.

**3. Why should conditions be tested with different values?**

Conditions should be tested with different values to make sure the script works correctly in different situations.

**4. How can conditionals help in automation scripts?**

Conditionals help automation scripts make decisions and perform different actions depending on the situation or input.

# Task 8 — Functions: Final Bash Automation Script

## Goal

Create a final Bash script using functions to organize reusable code.

### Evidence

#### Screenshot 1 — Content of `final-automation.sh`

Add your screenshot here.

---

#### Screenshot 2 — Output of `./final-automation.sh`

Add your screenshot here.

---

#### Screenshot 3 — Output of `ls -lah` showing all created scripts

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What is a function in Bash?**

A function in Bash is a reusable block of commands that performs a specific task.

**2. Why are functions useful in scripts?**

Functions make scripts more organized and easier to read. They also allow us to reuse the same code whenever needed.

**3. Which functions did you create in this script?**

I created four functions: show_user, check_score, check_files, and show_tools.

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

The script uses variables to store information, an array to store the list of tools, a loop to display the tools, conditionals to check the score and file status, and functions to organize these tasks into reusable sections.

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- All script files must be created and run successfully
- Required notes must be answered clearly for every task
- Do not expose sensitive information (keys, passwords, credentials)

---

# Completion Checklist

- [ ] Task 1: Environment setup verified, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: First script created, executed, permissions verified (Screenshots 1–3, Notes answered)
- [ ] Task 3: Variables script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 4: Arrays and loops script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 5: Counter loop script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 6: File validation script created and run (Screenshots 1–3, Notes answered)
- [ ] Task 7: Pass/Retry conditional script tested with both values (Screenshots 1–4, Notes answered)
- [ ] Task 8: Final automation script created and run (Screenshots 1–3, Notes answered)
- [ ] All scripts run without errors
- [ ] Full Name visible in all required screenshots
- [ ] LinkedIn post published and URL submitted
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
