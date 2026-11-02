# Module 00 — Your lab

**Goal:** have an isolated Linux to study in, and know why it needs to be isolated.

**Prerequisites:** none. Claude Code installed and onboarding done.

**Why it matters for the course:** security is learned by breaking things. Breaking things
on the machine that holds your bank, your email and your work is the first security
mistake you can make. The lab is the course's first security control.

---

## Lesson 0.1 — What an isolated study environment is

**Anchor concept:** a lab is an environment separated from the main machine, where a
mistake or malicious code cannot reach what matters. Isolating means limiting the
possible damage.

### Opening

1. Imagine you download a program from the internet that promises to "test the security of
   your network", and it is malicious. What can it reach if you run it on your everyday
   computer?
   - A good answer contains: the user's files, passwords saved in the browser, open
     sessions, other machines on the home network. Naming two is enough.
2. Why doesn't a doctor who studies dangerous viruses do it in their home kitchen?
   - A good answer contains: the damage escapes the place where it was contained; the
     lab has barriers that limit its reach.
3. What kind of "wall" do you imagine you can build inside a computer?
   - A good answer contains: any idea of separation, such as another user, another
     machine, a virtual machine or a container. It does not need to be precise: it is a
     curiosity question.

### Mission

No code in this lesson. With Claude, the student takes an inventory: what exists on their
machine today that a malicious program could reach. The student drives the investigation:
decides where to look and asks Claude for the commands to look.

Specification questions:
1. Which categories of valuable things will you look for?
   - A good answer contains: at least three categories, such as documents, credentials and
     sessions, SSH keys or tokens, devices on the network.
2. How will you know the inventory is good enough?
   - A good answer contains: a stopping criterion, such as "a list of what exists and
     where it is, for each category".

### Verification

1. From the inventory, which item would be the worst to leak, and why?
   - A good answer contains: a concrete item and the impact: what someone would do with it.
2. If the lab is a virtual machine inside this same computer, what would still be shared
   between the two?
   - A good answer contains: the hardware, the network, and the possibility of shared
     folders. The isolation is strong, but not absolute.

### Tool

Present the two lab options that lesson 0.2 will set up: **WSL2** (Linux inside Windows,
light, less isolated) and **VirtualBox** or similar (a full virtual machine, heavier, more
isolated). Ask: "From what you saw today, which one isolates more, and which one would you
use to run real malware?"

### Explain back

"Explain to a friend why you are not going to study attacks on your everyday machine."
Criterion: talks about limiting the reach of the damage and names at least one concrete
thing that would stay protected.

### For Socrates

- **Common mistakes:** thinking antivirus replaces isolation; thinking "I have nothing of
  value". Undo it by asking which sessions are logged in in the browser right now.
- **Bridge to security:** isolation and damage containment (*blast radius*) come back in
  containers (18), cloud and IAM (20) and sandboxed AI agents (38.3).

---

## Lesson 0.2 — Setting up Linux (WSL2 or VM)

**Anchor concept:** the lab is a whole operating system running on top of yours. Knowing
which of the two you are in, and what passes from one to the other, is the first skill of
anyone who works with isolation.

### Opening

1. What is an operating system? What is it for?
   - A good answer contains: the program that manages the hardware and lets the other
     programs use CPU, memory, disk and network without each one having to control the
     hardware on its own.
2. How can two operating systems run at the same time on the same computer?
   - A good answer contains: some idea of a layer that splits the hardware or pretends to
     be hardware. The word "hypervisor" is not required.

### Mission

Install the lab, with Claude as a guide, and prove it works. On Windows, the
recommendation is WSL2 with Ubuntu. If the student already uses Linux, a VM in VirtualBox.
The student asks Claude for the steps, but must understand what each command does before
running it.

Specification questions:
1. Before asking Claude for the steps: what do you need to tell it about your machine so
   the steps fit?
   - A good answer contains: the operating system and its version, and what the student
     wants as a result (which Linux, and what for).
2. How will you prove the lab is working?
   - A good answer contains: a concrete test, such as opening the Linux terminal and
     running a command that shows the system's name.

With the lab ready, the student runs `uname -a`, `whoami` and `pwd` inside it and explains
what each one showed.

### Verification

1. Create a file inside Linux. Can you see it from Windows (or from the main system)? And
   the other way around? Before testing: what do you predict?
   - A good answer contains: a prediction before the test. In WSL2, the two sides see each
     other (`\\wsl$` on one side and `/mnt/c` on the other). The student should conclude
     that WSL2 is not strong isolation.
2. If a malicious program runs inside your WSL2, does it reach your Windows documents?
   Why?
   - A good answer contains: yes, through `/mnt/c`. That is why WSL2 is fine for studying,
     but not for running real malware.

### Tool

The `wsl` command (or the VirtualBox panel): list, stop and export the distribution.
Question: "How would you bring the lab back to a clean state if you broke everything?"
Connects to snapshots, which come back in module 17.

### Explain back

"Explain where your Linux is running and what it shares with your machine." Criterion:
says it is one system running on top of the other and names at least one point of contact
(files, network).

### For Socrates

- **Common mistakes:** copying the install commands without reading them. If the student
  pastes a command without explaining it, stop and ask for the explanation of that
  command. It is also common to confuse the Windows terminal with the Linux one: ask the
  student to show the output of `uname`.
- **Bridge to security:** the question "what crosses the boundary?" is the same one in
  every trust boundary analysis (21.3).

---

## Lesson 0.3 — First conversation with Claude as an architect

**Anchor concept:** whoever specifies decides. A complete specification says what goes in,
what comes out, what happens and how to know it worked. What it does not say, the AI
decides in the student's place.

### Opening

1. You ask a builder to "make a wall". What can go wrong?
   - A good answer contains: the builder decides the height, material and place; the
     result may not serve what the student wanted.
2. When you ask the AI for something without details, who decides what was missing?
   - A good answer contains: the AI, by assumption. The student does not find out what it
     decided unless they read the result.

### Mission

The student asks Claude for a script of up to 20 lines that counts how many files exist in
a folder. Socrates does not accept the first request if it is vague: it asks the
specification questions until the request is complete. Then the student reads the script
before running it.

Specification questions:
1. What does the script receive?
   - A good answer contains: a folder, and how it is given (an argument or the current
     folder).
2. What counts as a "file"? Do folders count? And subfolders?
   - A good answer contains: an explicit decision. Any one works, as long as it is the
     student's.
3. What does the script show at the end?
   - A good answer contains: the output format, for example just the number or a sentence.
4. How will you test it?
   - A good answer contains: a folder with a known number of files, to compare with the
     result.

### Verification

1. Point to the line in the script that does the counting. What does it do?
   - A good answer contains: the right line and a rough explanation of the command.
2. What happens if you pass a folder that does not exist? Predict before testing.
   - A good answer contains: a prediction. After the test, the student concludes whether
     the script handles the error or not, and whether that was in the specification.
3. What decision did Claude make that you did not specify?
   - A good answer contains: something real from the script, such as the language chosen,
     hidden files or the error message. This is the most important question of the lesson.

### Tool

Claude Code itself: plan mode (Claude proposes a plan before writing code) and the habit
of asking "explain to me what you are going to do before doing it". Question: "For what
kind of task would you ask for the plan before the code?"

### Explain back

"Explain what a good specification needs to have, and what happens when it doesn't."
Criterion: names input, output, behavior and test, and says that whatever is missing, the
AI decides for the student.

### For Socrates

- **Common mistakes:** thinking the AI "knows what I meant". Verification question 3
  undoes this: there is always a decision the student did not make.
- **Bridge to security:** AI-generated code with decisions nobody reviewed is one of the
  sources of vulnerabilities in the AI era (14.3, 40.2). Reviewing what the AI decided is a
  security task.
