

# Part 1 — DevOps Fundamentals

## Task 1: Problems and DevOps Solutions




**Problem 1: Slow Deployment**

Developers complete features in two weeks, but the Operations team deploys every three months. This causes delays.

**Solution:** DevOps uses Continuous Integration and Continuous Delivery (CI/CD) to automate testing and deployment. This allows smaller and faster releases.

**Problem 2: Lack of Communication**

Developers and Operations teams blame each other instead of working together.

**Solution:** DevOps promotes teamwork, shared responsibility, regular communication, and collaboration between teams.

## Task 2: Eight Stages of the DevOps Lifecycle

1. **Plan:** Decide project requirements. Tool: GitHub Issues.
2. **Code:** Write and manage source code. Tool: Git.
3. **Build:** Convert source code into a working application. Tool: Maven.
4. **Test:** Check the application for errors. Tool: JUnit.
5. **Release:** Prepare the application for deployment. Tool: Git Tags.
6. **Deploy:** Install the application on a server. Tool: Ansible.
7. **Operate:** Manage and maintain the application. Tool: Linux.
8. **Monitor:** Check application performance and errors. Tool: journalctl.

## Task 3: CALMS Framework

1. **Culture:** Promote teamwork and communication. Action: Hold regular team meetings.
2. **Automation:** Automate repetitive tasks. Action: Use scripts for testing and deployment.
3. **Lean:** Reduce waste and unnecessary work. Action: Complete tasks in small steps.
4. **Measurement:** Measure team and application performance. Action: Track deployment frequency.
5. **Sharing:** Share knowledge and information. Action: Share notes and code with team members.

## Task 4: DORA Metrics and Three Ways

**Four DORA Metrics:**

1. Deployment Frequency — How often an application is deployed. (Speed)
2. Lead Time for Changes — Time taken to move code from commit to production. (Speed)
3. Change Failure Rate — Percentage of deployments that cause failures. (Stability)
4. Failed Deployment Recovery Time — Time needed to recover from a failed deployment. (Stability)

**The Three Ways of DevOps:**

1. **Flow:** Improve the flow of work from development to operations.
2. **Feedback:** Get quick feedback to identify and fix problems.
3. **Continual Learning:** Learn from mistakes and continuously improve.

# Part 2 — Linux Commands

## Task 1: Create Directory Structure

**Commands:**
```bash
mkdir -p ~/assignment/linux/data/reports
mkdir -p ~/assignment/linux/data/archive
ls -R ~/assignment/linux
```

**Actual Output:**
```text
/home/rafay/assignment/linux:
data

/home/rafay/assignment/linux/data:
archive  reports

/home/rafay/assignment/linux/data/archive:

/home/rafay/assignment/linux/data/reports:
```

**Explanation:** The mkdir -p command creates directories, including parent directories. The ls -R command displays directories and their contents recursively.
## Task 2: File Permissions

**Commands:**
```bash
cd ~/assignment/linux
touch report.txt run.sh
chmod 640 report.txt
chmod 754 run.sh
ls -l report.txt run.sh
```

**Actual Output:**
```text
-rw-r----- 1 rafay rafay 0 report.txt
-rwxr-xr-- 1 rafay rafay 0 run.sh
```

**Explanation:**
- 640: Owner can read and write, group can read, others have no permission.
- 754: Owner can read, write and execute; group can read and execute; others can read.

**Screenshot:** `screenshots/p2t2.png`
## Task 3: Working with Log Files

**Commands:**
```bash
printf 'INFO start\nERROR disk full\nINFO user login\nWARN slow response\nERROR timeout\nINFO user logout\nERROR disk full\nINFO backup done\nWARN memory high\nERROR timeout\nINFO restart\nERROR disk full\n' > server.log

grep 'ERROR' server.log | wc -l
grep 'WARN' server.log | wc -l
grep 'ERROR' server.log | grep 'disk'
```

**Actual Output:**
```text
5
2
ERROR disk full
ERROR disk full
ERROR disk full
```

**Explanation:** The grep command searches for matching text. The pipe (`|`) sends the output of one command to another. The wc -l command counts the number of matching lines.

## Task 4: Managing Processes

**Commands:**

```bash
# Start a background process
sleep 600 &

# Find the running process
ps -ef | grep '[s]leep 600'

# Terminate the first process gracefully
kill 132

# Start another background process
sleep 600 &

# Find both running processes
ps -ef | grep '[s]leep 600'

# Forcefully terminate the second process
kill -9 135

# Verify that the processes have stopped
ps -p 132
ps -p 135
```

**Actual Output:**

```text
[1] 132
rafay 132 ... sleep 600

[2] 135
rafay 132 ... sleep 600
rafay 135 ... sleep 600

  PID TTY          TIME CMD
  PID TTY          TIME CMD
```

**Explanation:**

- `sleep 600 &` starts a process in the background.
- `ps -ef` displays running processes.
- `grep` searches for a specific process.
- `kill 132` sends a termination signal to stop a process gracefully.
- `kill -9 135` forcefully terminates a process.
- `ps -p` checks whether a process is still running.

**Difference:** `kill` requests a graceful termination, while `kill -9` forcefully stops the process.

**Screenshot:** `screenshots/p2t4.png`

## Task 5: User and Permissions

**Commands:**

```bash
whoami
groups
sudo apt update
apt list --upgradable
```

**Actual Output:**

```text
whoami:
rafay

groups:
rafay adm dialout cdrom floppy sudo audio dip video plugdev netdev

sudo apt update:
Fetched 28.4 MB in 26s
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
84 packages can be upgraded.

apt list --upgradable:
Listing... Done
84 packages are available for upgrade.
```

**Explanation:**

- `whoami` displays the current logged-in username.
- `groups` displays all groups the user belongs to.
- `sudo` allows a normal user to execute commands with administrator privileges.
- `apt update` refreshes the package information from repositories.
- `apt list --upgradable` displays packages that have available updates.

**Conclusion:** The user has sudo privileges and can manage system packages using administrative commands.




## Part 3 – Git and GitHub

### Task 1 – Connect Local Repository to GitHub

Commands:
```bash
git remote add origin https://github.com/arafayZ/devops-assignment-1.git
git remote -v
git push -u origin main
```

The local repository was successfully connected to GitHub, and the main branch was pushed to the remote repository.

### Task 2 – Create and Merge a Feature Branch

Commands:
```bash
git switch -c feature-notes
git branch
nano notes.md
git add notes.md
git commit -m "Add DevOps notes on feature branch"
git switch main
git merge feature-notes
git push
```

The feature-notes branch was created. A notes.md file was added and committed. The branch was successfully merged into main using a fast-forward merge.

### Task 3 – Resolve a Merge Conflict

Commands:
```bash
git switch -c conflict-branch
nano conflict.txt
git add conflict.txt
git commit -m "Update project maintainer on conflict branch"
git switch main
nano conflict.txt
git add conflict.txt
git commit -m "Update project maintainer on main branch"
git merge conflict-branch
```

Git reported a content conflict because both branches modified the same line in conflict.txt.

The conflict was resolved manually by keeping both changes:

```text
This project is maintained by the IT Department and DevOps team.
```

The resolved file was staged and committed:

```bash
git add conflict.txt
git commit -m "Resolve merge conflict in conflict.txt"
git log --oneline --graph --all -6
```

The merge was completed successfully.

**Screenshots:**
- screenshots/p3t1.png – Branch creation
- screenshots/p3t2.png – Feature branch merge
- screenshots/p3t3.png – Merge conflict resolution






### Task – Understanding the Three Git Areas

**1. Working Directory:**  
The working directory is where we create, edit, and modify project files.

**2. Staging Area:**  
The staging area contains changes selected for the next commit. We use `git add` to move changes into this area.

**3. Repository:**  
The repository stores committed changes and maintains the project's version history.

**Commands used:**
```bash
git status
git add README.md
git commit -m "Update README with assignment details"
git push origin main
```
