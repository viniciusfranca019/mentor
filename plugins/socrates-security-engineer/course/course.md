# Course: Security Engineer in the age of AI

## Who it is for

For people with an IT degree (for example, a technologist degree in Systems Analysis and
Development) but little practice in programming, networks, virtualization and
infrastructure. The expected starting point: they have heard of almost everything, but
learned it by the tool's name, not by how it works underneath.

## Where you get to

By the end, the student:

- explains how a computer, a network and a web application work inside;
- reads and writes code with AI's help, knowing how to steer and review what the AI produces;
- designs a system's architecture and finds its trust boundaries;
- models threats, and finds and fixes the most common vulnerabilities;
- detects and responds to incidents from logs;
- understands the new risks of systems with LLMs and agents, and uses AI for defense.

## Course principle

**A tool is a shortcut for something you already understand.** Every module builds the
foundation before showing the tool. A security engineer is called precisely when the
tool is not enough: when the scanner finds nothing, the log makes no sense, or the attack
is new. Someone who only knows the button has nowhere to go at that point.

In the age of AI this counts double: Claude is the most powerful tool the student will
use, and also the easiest one to turn into a crutch. Here the student uses AI all the
time, but always as the architect who specifies and reviews.

## Axes and diagnosis

The course's axes and the question ladder for each one. How to use the ladder is in
`<root>/skills/socrates/references/levels.md`.

| Axis | Track phases |
|------|--------------|
| Systems | 1. The machine |
| Networks | 2. The network |
| Building with AI | 3. Building with AI |
| Infrastructure | 4. Architecture and infrastructure |
| Security | 5 to 8, and the final project |

### Systems

- **R:** What is a process?
  - Layer 2: a running program, with its own memory and resources.
- **M:** You double-click a program. What happens inside the computer until the window
  appears? Tell it however you can.
  - Layer 3: the file goes from disk to memory, the operating system creates the
    process and shares the CPU and memory between it and the others. In their own words.
- **D:** A program that worked yesterday now says "permission denied" when opening a file.
  Where do you investigate, and how would you fix it without opening the file to everyone?
  - Layer 4: concrete hypotheses: the file's owner and permissions changed, the program
    runs as another user, the path changed.
  - Layer 5: give the permission only to whoever needs it, and why opening it to everyone
    or running as administrator is costly.
- **D2:** A program gets slower and slower until it freezes the machine, and only goes back
  to normal after a reboot. Where do you investigate, and what would you do?
  - Layer 4: looks at the process's memory and CPU use over time and suspects a memory
    leak or a process that multiplies.
  - Layer 5: compares restarting the program periodically, limiting its memory and
    fixing the cause, and the cost of each.

### Networks

- **R:** What is an IP address?
  - Layer 2: the address that identifies a machine on the network, so data reaches it.
- **M:** You type a site's address and press Enter. How does the computer find out where
  to send the request, and what comes back?
  - Layer 3: the name becomes an IP (DNS), the computer opens a connection to that IP and
    sends an HTTP request, the server returns the page.
- **D:** The site opens when you type the IP, but not by its name. Where do you look for
  the problem, and which fix would you choose?
  - Layer 4: the problem is in the name translation: the configured DNS server, the cache,
    or a `hosts` file that overrides the name.
  - Layer 5: compares the fixes, such as changing the DNS, clearing the cache or editing
    `hosts`, and the cost of each.
- **D2:** Your computer reaches websites normally, but cannot reach the printer on your
  home network. Where do you look, and what would you change?
  - Layer 4: hypotheses on the local network: the printer changed IP, it is on another
    network, or a firewall blocks it.
  - Layer 5: compares fixing the printer's IP, reserving it on the router or using the
    name, and the cost of each.

### Building with AI

- **R:** What is a function in a program?
  - Layer 2: a named piece of code that takes inputs, does a task and returns a result.
- **M:** You ask Claude for a script that reads a file and counts the lines. Before
  running it, how do you check that it does what you asked?
  - Layer 3: read the code and find the part that counts, predict the output for a file
    they know, and test with that file.
- **D:** The script works on your file, but breaks on a colleague's file. How do you find
  the cause, and do you fix the code or ask the AI again? Why?
  - Layer 4: compare the two inputs (empty file, encoding, line breaks, path) and
    reproduce the error with the smallest possible input.
  - Layer 5: fix it by understanding the cause, or ask again telling the AI the cause, and
    the risk of asking again without knowing the cause.
- **D2:** The AI wrote a function that works, but you don't understand part of it. The
  code goes to production tomorrow. What do you do?
  - Layer 4: isolates the piece and tests it with inputs to see what it really does.
  - Layer 5: decides between rewriting it in a way they understand, asking for an
    explanation and checking it, or delaying the delivery, and the risk of each.

### Infrastructure

- **R:** What is a container?
  - Layer 2: a way to package and run an application in isolation, with everything it
    needs.
- **M:** What is the difference between a virtual machine and a container? What does each
  one isolate?
  - Layer 3: the virtual machine has a whole operating system on top of a hypervisor; the
    container shares the machine's kernel and isolates processes and files.
- **D:** An application in a container needs the database password. Where do you keep
  that password, and what changes if someone breaks into the container?
  - Layer 4: the places where the password leaks: inside the image, in the code, in a
    visible environment variable, in the log.
  - Layer 5: compares environment variable, mounted file and secrets vault, and states the
    damage of each if the container is broken into.
- **D2:** An application works on your machine but not on the server. Both run the same
  container. Where do you look?
  - Layer 4: what is outside the image: environment variables, volumes, network, the
    kernel version or the processor architecture.
  - Layer 5: compares moving the configuration into the image or keeping it outside, and
    the cost of each.

### Security

- **R:** What is a vulnerability?
  - Layer 2: a flaw in a system that someone can use to do what they should not.
- **M:** A site has a login. How could someone get into another person's account without
  knowing their password?
  - Layer 3: a concrete, explained path: stealing the session (the cookie), reusing a
    password leaked from another site, tricking the person with phishing, or a flaw that
    shows someone else's account by changing a number in the address.
- **D:** A company's chatbot reads customers' emails and can send replies. What risk does
  this create, and how would you reduce it without turning the chatbot off?
  - Layer 4: an email can carry instructions the model obeys (indirect prompt injection)
    and make the chatbot leak data or send what it should not.
  - Layer 5: mitigation through architecture, such as human approval before sending, only
    the necessary permissions, and separating what is data from what is instruction, with
    the cost of each.
- **D2:** An employee gets an email from "support" asking them to install a program. They
  installed it. What do you investigate first, and what do you do now?
  - Layer 4: what the program did: processes, network connections, accounts used, what
    it reached on the machine and on the network.
  - Layer 5: compares isolating the machine, changing the passwords and investigating
    first, and the cost of each order.

## Track

A lesson takes 30 to 60 minutes. The `planned` modules will be published in upcoming
versions of the plugin.

### Phase 1 — The machine

By the end: knows what happens inside a computer when a program runs, and operates a
Linux machine from the terminal.

| # | Module | Lessons | Status |
|---|--------|---------|--------|
| 00 | Your lab | 0.1 What an isolated study environment is · 0.2 Setting up Linux (WSL2 or VM) · 0.3 First conversation with Claude as an architect | available |
| 01 | How the computer represents things | 1.1 Everything is a number: bits, bytes and hexadecimal · 1.2 Text is a number too: encoding · 1.3 Files and formats: the extension lies · 1.4 From code to program: compiled and interpreted | available |
| 02 | Processes and memory | 2.1 Program vs process · 2.2 A process's memory · 2.3 Processes talking: signals and pipes · 2.4 What a service (daemon) is | planned |
| 03 | The Linux shell | 3.1 What the shell does with what you type · 3.2 File system and paths · 3.3 Input, output and redirection · 3.4 Environment variables and PATH · 3.5 Find and filter: find, grep, pipes | planned |
| 04 | Users, permissions and privilege | 4.1 Users and groups · 4.2 rwx permissions · 4.3 root and sudo · 4.4 setuid and privilege escalation | planned |

### Phase 2 — The network

By the end: explains the path of a request from the browser to the server, layer by layer.

| # | Module | Lessons | Status |
|---|--------|---------|--------|
| 05 | Addresses and routing | 5.1 Why layers exist · 5.2 IP address and mask · 5.3 Routing and gateway · 5.4 NAT and private IP | planned |
| 06 | Transport: TCP and UDP | 6.1 Ports · 6.2 The TCP handshake · 6.3 Reliability vs speed: UDP · 6.4 Sockets: the network as the program sees it | planned |
| 07 | DNS | 7.1 Names become addresses · 7.2 The server hierarchy · 7.3 Cache and TTL · 7.4 Attacks on DNS | planned |
| 08 | HTTP | 8.1 Request and response · 8.2 Methods and status · 8.3 Headers · 8.4 Cookies and state | planned |
| 09 | TLS | 9.1 The open channel problem · 9.2 The TLS handshake · 9.3 Certificates and the chain of trust · 9.4 What TLS does not protect | planned |

### Phase 3 — Building with AI

By the end: steers Claude to build small programs and reads the generated code with
security in mind.

| # | Module | Lessons | Status |
|---|--------|---------|--------|
| 10 | Reading Python code | 10.1 Variables, types and flow · 10.2 Functions · 10.3 Data structures · 10.4 Errors and exceptions | planned |
| 11 | Git | 11.1 What a version is · 11.2 Commit, branch and merge · 11.3 Remote and GitHub · 11.4 What never goes into Git | planned |
| 12 | Automation with shell and Python | 12.1 Shell scripts · 12.2 Reading and processing files · 12.3 Calling programs and APIs | planned |
| 13 | APIs | 13.1 What an API is · 13.2 REST and JSON · 13.3 Building a small API · 13.4 Consuming an API | planned |
| 14 | Testing and reviewing AI-generated code | 14.1 Why test · 14.2 Writing a test · 14.3 Reviewing what the AI wrote | planned |

### Phase 4 — Architecture and infrastructure

By the end: designs a real system with client, server, database, containers and cloud,
and points out where the data and the access are.

| # | Module | Lessons | Status |
|---|--------|---------|--------|
| 15 | Architecture of a web application | 15.1 Client, server and database · 15.2 State and session · 15.3 Queues and services | planned |
| 16 | Databases and SQL | 16.1 Tables and queries · 16.2 Relationships · 16.3 Who accesses the database | planned |
| 17 | Virtualization | 17.1 Hypervisor and VM · 17.2 Isolation and what escapes it · 17.3 Snapshots and a disposable lab | planned |
| 18 | Containers | 18.1 Namespaces and cgroups · 18.2 Image vs container · 18.3 Docker in practice · 18.4 A container is not a VM | planned |
| 19 | Orchestration | 19.1 Why Kubernetes exists · 19.2 Pods, services and secrets · 19.3 The cluster's attack surface | planned |
| 20 | Cloud and IAM | 20.1 The shared responsibility model · 20.2 Identities and policies · 20.3 Least privilege in practice · 20.4 Buckets and exposed data | planned |

### Phase 5 — Security fundamentals

By the end: thinks like an attacker and like a defender about any system they see.

| # | Module | Lessons | Status |
|---|--------|---------|--------|
| 21 | Thinking about security | 21.1 Confidentiality, integrity and availability · 21.2 Assets, threats and risks · 21.3 Trust boundaries | planned |
| 22 | Threat modeling | 22.1 Data flow diagram · 22.2 STRIDE · 22.3 Prioritizing risks | planned |
| 23 | Identity | 23.1 Authentication vs authorization · 23.2 Passwords and hashing · 23.3 Sessions and tokens · 23.4 OAuth and OIDC · 23.5 MFA | planned |
| 24 | Applied cryptography | 24.1 Hashing · 24.2 Symmetric · 24.3 Asymmetric and signatures · 24.4 Common crypto mistakes | planned |
| 25 | Secrets | 25.1 Where secrets leak · 25.2 Secrets vaults · 25.3 Rotation and leak response | planned |

### Phase 6 — Application security

By the end: finds, exploits in a lab and fixes the most common vulnerabilities in web
applications.

| # | Module | Lessons | Status |
|---|--------|---------|--------|
| 26 | Injection | 26.1 Data that becomes a command · 26.2 SQL injection · 26.3 Command injection · 26.4 The right fix | planned |
| 27 | Access control | 27.1 IDOR · 27.2 Horizontal and vertical escalation · 27.3 Authorization in the right place | planned |
| 28 | Browser attacks | 28.1 Same-origin policy · 28.2 XSS · 28.3 CSRF · 28.4 CORS | planned |
| 29 | SSRF and trust in the server | 29.1 The server as a middleman · 29.2 SSRF · 29.3 Cloud metadata | planned |
| 30 | Software supply chain | 30.1 Dependencies · 30.2 Malicious packages · 30.3 SBOM and signing | planned |
| 31 | Code review and security testing | 31.1 Code review with an attacker's eye · 31.2 SAST · 31.3 DAST · 31.4 Pentesting an application | planned |

### Phase 7 — Defense and operations

By the end: builds a system's visibility, detects an attack in the logs and leads the
response.

| # | Module | Lessons | Status |
|---|--------|---------|--------|
| 32 | Logs and observability | 32.1 What to log · 32.2 Centralizing logs · 32.3 Logs that leak data | planned |
| 33 | Detection | 33.1 From log to alert · 33.2 Writing a detection rule · 33.3 False positives and false negatives | planned |
| 34 | Incident response | 34.1 The response cycle · 34.2 Containment and evidence · 34.3 Post-incident | planned |
| 35 | Hardening | 35.1 Linux · 35.2 Containers · 35.3 Network and firewall | planned |

### Phase 8 — Security in the age of AI

By the end: understands the risks of systems with LLMs and agents, attacks and protects
an agent in a lab, and uses AI for defense.

| # | Module | Lessons | Status |
|---|--------|---------|--------|
| 36 | How an LLM works | 36.1 Tokens and context · 36.2 Why the model does not separate instruction from data · 36.3 Hallucination and trust | planned |
| 37 | Prompt injection | 37.1 Direct injection · 37.2 Indirect injection: the document that gives orders · 37.3 Why no perfect filter exists · 37.4 Mitigations through architecture | planned |
| 38 | Agents, tools and MCP | 38.1 What an agent can do · 38.2 Excessive autonomy · 38.3 Permissions and sandbox · 38.4 MCP: servers and trust | planned |
| 39 | Data and models | 39.1 Data leaks through the LLM · 39.2 Data poisoning · 39.3 Supply chain of models and plugins (this one included) | planned |
| 40 | AI for defense | 40.1 Alert triage with AI · 40.2 Code review with AI · 40.3 The limits: when not to trust | planned |

### Final project

| # | Module | Lessons | Status |
|---|--------|---------|--------|
| 41 | Final project | 41.1 Building an application with an agent · 41.2 Modeling the threats · 41.3 Attacking · 41.4 Fixing and writing the report | planned |
