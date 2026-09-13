# Week 00 - Internet and Networking

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

# 🧑‍💻 Task 1: Using ChatGPT as Your Learning Assistant

## Scenario

You're new to DevOps and will frequently encounter technical questions. ChatGPT can be your learning companion.

## Your Task

Write a clear ChatGPT prompt to help you understand:

> "What is a protocol in networking? Explain with a simple real-life example."

Take a screenshot of your interaction showing:

* Your detailed prompt (with clear expectations)
* ChatGPT's simplified response with an example

## Screenshot

Save your screenshot in the `screenshots` folder and update the file name below.

![Task 1 Screenshot](screenshots/<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2db57abf-2d24-4a8a-b24d-8cc39c5c58f0" />
)


Replace `task-1-chatgpt.png` with your actual screenshot file name.

---

## What I Learned (2–3 lines)

A networking protocol is a set of predefined rules and standards that devices follow to communicate and exchange data over a network. It defines how data is formatted, transmitted, received, and interpreted between communicating devices. Examples include TCP, IP, HTTP, HTTPS, DNS, and SSH.

# 🌐 Task 2: Internet and Networking

## Scenario

Your friend is launching an online bookstore named **EpicReads**.

He asked you to explain how users globally can access his website hosted in Finland.

## Your Task

Write a short explanation (**100–150 words**) that includes:

* Packet Switching
* IP Address
* TCP/IP
* HTTP/HTTPS

💡 **Tip:** You may use ChatGPT (as demonstrated in Task 1) to refine your explanation.

## Answer

Imagine a customer in India opening the EpicReads bookstore website, even though its server is located in Finland. When the customer enters the website address, the request is divided into small pieces called packets. This is known as **packet switching**, and the packets may take different routes through the Internet before reaching Finland. The **IP address** identifies the destination server so the request knows where to go. **TCP/IP** controls this communication: IP handles the addressing and routing, while TCP helps deliver the data properly and in the correct order. Once the connection reaches the EpicReads server, **HTTP/HTTPS** allows the browser and server to exchange website information. HTTPS is preferred because it encrypts the communication, making activities such as logging in and purchasing books safer.


# 🏗️ Task 3: Application Architecture & Stack

## Scenario

EpicReads bookstore has two application versions:

### Two-Tier Application

* Frontend
* Database

### Three-Tier Application

* Frontend
* Backend
* Database

## Your Task

* Draw simple diagrams (hand-drawn or tool-based such as draw.io)
* Label each layer clearly
* List at least two common technologies or tools used for each layer
* Submit a screenshot or photo clearly showing your own drawing

## Diagram Screenshot / Photo

Save your diagram image in the `screenshots` folder and update the file name below.

![Application Architecture Diagram](screenshots/<img width="1536" height="1024" alt="devops1" src="https://github.com/user-attachments/assets/9aa50eb2-fdc9-4b94-81f3-d87c68b15118" />
)


Replace `task-3-diagram.png` with your actual diagram file name.

---

## Technologies Used

### Frontend

React.js

HTML/CSS

### Backend

Node.js

Express.js

### Database

MySQL

MongoDB

---

# 🌍 Task 4: Domain Name & DNS (Basic Concepts)

## Scenario

Your friend's bookstore **EpicReads** is currently accessible through:

```text
52.172.142.222:3000
```

He purchased the domain:

```text
epicreads.com
```

## Your Task

In **50–100 words**, explain in your own words:

1. What is DNS (Domain Name System)?
2. Which DNS record type should be used to connect the domain to the given IP, and why?

## Answer

1. DNS is a system that converts human-readable domain names, such as epicreads.com, into IP addresses that computers use to locate servers. It makes websites easier to access because users don't have to remember numerical IP addresses.

2. An A (Address) record should be used because it connects a domain name to an IPv4 address. Since 52.172.142.222 is an IPv4 address, an A record can map:

epicreads.com → 52.172.142.222

So, when someone enters epicreads.com, DNS directs them to the server at that IP address.

# 💻 Task 5: Visual Studio Code Setup (Hands-on)

## Your Task

Install Visual Studio Code (if not already installed).

Take a screenshot of your VS Code environment showing:

* Terminal open inside VS Code
* Running a basic command:

### Windows

```powershell
dir
```

### Linux / macOS

```bash
pwd
ls
```

* Your selected VS Code theme clearly visible

⚠️ **Important:** The screenshot must show your username or another identifiable detail to confirm it is your environment.

## Screenshot

Save your screenshot in the `screenshots` folder and update the file name below.

![VS Code Setup Screenshot](screenshots/<img width="1920" height="1080" alt="Screenshot (67)" src="https://github.com/user-attachments/assets/2478f676-ee3d-4a83-9cd4-19f2aa254772" />
)


Replace `task-5-vscode.png` with your actual screenshot file name.

---

# 🔗 Task 6: Publish Your Assignment as a LinkedIn Post

## Objective

Publishing on LinkedIn helps you:

* Build your professional online presence
* Reinforce your learning
* Document your DevOps journey publicly

## Your Task

Summarize your answers from Tasks 1–5 into a LinkedIn post.

Clearly structure your post into the following sections:

* ChatGPT
* Internet & Networking
* App Architecture
* DNS
* VS Code Setup

Add the following credit note at the end of your post:

> **P.S. This post is part of the DevOps Micro Internship (DMI) with Agentic AI — Cohort 3 — by Pravin Mishra. My graded progress is public: https://dmi.pravinmishra.com/s/YOUR-GITHUB-USERNAME.html · Start your DevOps journey: https://dmi.pravinmishra.com/?utm_source=student&utm_medium=ps-linkedin&utm_campaign=cohort3**

---

## LinkedIn Post URL

Paste your LinkedIn post URL here:

https://www.linkedin.com/posts/amruthabandi_devops-devopslearning-dmi-activity-7504904494137344000-uG3m?utm_source=share&utm_medium=member_desktop&rcm=ACoAAFPDVrQBiRgPYVYtuI7TM3YhAKe2kcrI21o
---

## LinkedIn Post Backup Copy

Paste the full text of your LinkedIn post here:

🚀 Week 00 of my DevOps Journey | Internet & Networking
I’ve started my DevOps Micro Internship (DMI) — Cohort 3 with Agentic AI, and this week was focused on understanding the fundamentals of the Internet and networking.
Here’s what I worked on 👇
💬 ChatGPT
I explored how ChatGPT can be used as a learning assistant for technical topics. I learned about networking protocols and how they act as a set of rules that allow devices to communicate with each other.
🌐 Internet & Networking
I understood what happens when a user accesses a website hosted in another country. I learned about packet switching, IP addresses, TCP/IP, and HTTP/HTTPS, and how these work together when data travels across the Internet.
🏗️ App Architecture
I explored two-tier and three-tier application architectures. I learned how the frontend, backend, and database interact in a three-tier application and explored technologies such as React.js, Node.js, Express.js, MySQL, and MongoDB. I also created an architecture diagram using a diagramming tool.
🔗 DNS
I learned how DNS converts domain names into IP addresses, making websites easier to access. I also learned that an A record can connect an IPv4 address such as 52.172.142.222 with a domain like epicreads.com.
💻 VS Code Setup
I set up and worked with Visual Studio Code, opened its integrated terminal, practiced basic commands, and explored the development environment and theme customization.
This week gave me a better understanding of the fundamentals behind how websites communicate over the Internet and how applications are structured.
Looking forward to building on these basics and exploring Linux, servers, Git, Docker, CI/CD, cloud, and automation in the upcoming stages of my DevOps journey. 🚀
hashtag#DevOps hashtag#DevOpsLearning hashtag#DMI hashtag#AgenticAI hashtag#Networking hashtag#DNS hashtag#ApplicationArchitecture hashtag#VSCode hashtag#LearningJourney hashtag#TechStudent Pravin Mishra
P.S. This post is part of the DevOps Micro Internship (DMI) with Agentic AI — Cohort 3 — by Pravin Mishra. My graded progress is public: https://lnkd.in/dnMwXX96 Start your DevOps journey: https://lnkd.in/diYNBnCA

---

# Reflection – Week 0

### What did you find easy?

I found learning the basic concepts of networking and DNS relatively easy. Understanding how IP addresses, TCP/IP, HTTP/HTTPS, and domain names work together was interesting. Setting up VS Code and using its terminal was also easy.

---

### What was difficult?

The most difficult part was understanding how data actually travels between a user and a server through the Internet. I also found the difference between two-tier and three-tier application architecture a little confusing at first, but creating the diagrams helped me understand it better.
---

### What will you improve next week?

Next week, I want to improve my understanding of commands, servers, and networking concepts. I also want to practice more instead of only reading the concepts so that I can become more comfortable with DevOps tools and workflows.
---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.


## 📌 Resources

- 🌐 **DMI Official Website:** https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 **University:** https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 **Discord Community:** https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 **Blog:** https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ **YouTube Playlist (DMI Cohort 3):** https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 **Pravin Mishra (LinkedIn):** https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 **CloudAdvisory (LinkedIn):** https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track*
