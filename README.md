# My Linux Upskill Challenge Journal
BITA Kernel Crew · Cohort 1 · Sept 2026

# Day 0
- Digital Ocean VPS Set-up
    - This option for me was just out of curiosity from using a new tool product, as I have spent years learning on the most cheapest and effective VM out there which is Virtual Box aka my Go To for Labbing.
    
- Problems I hit and how I fixed them:
None so far. These are all refresher commands for me. I am not a System Admin so alot of these commands, while I have general knowledge of....they arent ones that I utilize to get my job (cloud engineer), none the less Give me all the Linux tools to the kingdom. Im here for it!


# Day 1 - Get to know your server
Where do we start:  SSH and log into the server that you created.  COMMAND: SSH user@IPADDRESS 
Once inside the server, the main agenda is to get comfortable and learn certain commands and what they do.
### Commands
- lsb_releaase - shows the what Linux flavor and version that you are in.
- uname -a - prints the system information
- uptime - gives you the time of how long your system has been running
- whoami - Not da girls dem sugar!  seriously....this is the username that is currently logged into the system.
- lshw - will give you a whole lot of information on the hardware configuration
- free -h - is used to check the amount of memory that they system has used
- vmstat - will spit out memory statistics that you will only care about if you are running high operations on the server.
- top - is going to give you a real time synopsis over the systems that are currently running in the system and how much usage, time, memory, etc that it is using...Tip: You have to CTL C out to get back to the Command line.
- df -h - is how much disk space that is free and being used.
- du -h - will give you an overview of the size of the listed folders
- ip addr - this is going to give you the overview of your network connections also known as interfaces and host ip's. 

# Day 2 - Basic Navigation
This is my jam! Honestly this is how I have survived using Linux and is absolutely the foundation to understanding and using the command line intentionally.

### Navigating the Linux File Structure

Linux organizes files and directories in a tree structure beginning at the **root directory (`/`)**.

Everything on the system exists somewhere underneath `/`.

Common directories include:

* `/etc` — System configuration files
* `/home` — User home directories
* `/var` — Variable data
* `/var/log` — System and application logs

To learn more about the Linux directory structure:

```bash
man hier
```

---

### Where Am I? — `pwd`

You are always working inside a directory.

Use:

```bash
pwd
```

`pwd` means **Print Working Directory** and displays your current location.

Example:

```text
/home/student
```

> **Beginner Tip:** If you get lost, run `pwd`.

---

### Moving Around — `cd`

Use `cd` (**Change Directory**) to move to another directory.

```bash
cd /var/log
```

Verify your location:

```bash
pwd
```

Move **up one directory**:

```bash
cd ..
```

Example:

```text
/var/log → cd .. → /var → cd .. → /
```

Return to your home directory:

```bash
cd
```

or:

```bash
cd ~
```

---

### Absolute vs. Relative Paths

An **absolute path** starts from the root directory `/`:

```bash
cd /var/log
```

A **relative path** starts from your current location.

For example, if you are already in `/var`:

```bash
cd log
```

This also takes you to `/var/log`.

```text
Absolute = Start from /
Relative = Start from where I am now
```

---

### Viewing Files — `ls`

Use `ls` to see the contents of a directory:

```bash
ls
```

Useful options:

```bash
ls -l       # Detailed listing
ls -a       # Include hidden files
ls -ltra    # Detailed listing, hidden files, sorted by time
```

Files beginning with `.` are considered **hidden files**.

Examples:

```text
.bashrc
.gitconfig
.gitignore
```

Use the following to display them:

```bash
ls -a
```

When using `ls -l`, the first character helps identify the file type:

```text
drwxr-xr-x    # d = directory
-rw-r--r--    # - = regular file
```

---

### Understanding Command Syntax

Consider:

```bash
ls -l /var/log
```

This breaks down into:

```text
ls          -l          /var/log
│            │              │
Command    Option        Argument
```

* **Command** — What Linux should do
* **Option** — Changes how the command behaves
* **Argument** — What the command should operate on

Therefore:

```bash
ls -l /var/log
```

means:

> List the contents of `/var/log` using the long listing format.

---

### Quick Reference

| Command        | Purpose                                 |
| -------------- | --------------------------------------- |
| `pwd`          | Show the current directory              |
| `ls`           | List files and directories              |
| `ls -l`        | Display a detailed listing              |
| `ls -a`        | Show hidden files                       |
| `ls -ltra`     | Detailed listing including hidden files |
| `cd /path`     | Move to a directory                     |
| `cd ..`        | Move up one directory                   |
| `cd` or `cd ~` | Return to your home directory           |
| `man hier`     | View the filesystem hierarchy manual    |

---

### Quick Practice

```bash
pwd
ls
cd /var/log
pwd
ls -l
cd ..
pwd
cd
```

### Four Commands to Remember

```bash
pwd       # Where am I?
ls        # What's here?
cd        # Go somewhere
cd ..     # Go up one level
```

Mastering these basic commands provides the foundation for navigating Linux and working with configuration files, logs, users, services, permissions, and other system administration tasks.

# Day 3 — Sudo and Administrative Privileges

Linux separates **regular user access** from **administrative access**. Understanding `root` and `sudo` is essential because many system-level changes require elevated privileges.

---

### Linux User Types

There are three basic levels of users to understand:

* **root** — The superuser with unrestricted access to the system.
* **sudo users** — Regular users authorized to run administrative commands using `sudo`.
* **regular users** — Users who normally manage only their own files, directories, and environment.

Check which user you are currently logged in as:

```bash
whoami
```

Example:

```text
student
```

---

### Avoid Working Directly as Root

The `root` account can modify or delete virtually anything on the system. A mistake while operating as root can therefore affect the entire system.

Instead, the preferred approach is to log in with a regular administrative account and elevate privileges only when necessary:

```bash
sudo <command>
```

For example:

```bash
sudo systemctl restart sshd
```

This runs the command with elevated privileges without requiring you to remain logged in as `root`.

---

### Understanding `sudo`

`sudo` means **superuser do** and allows an authorized user to execute commands with elevated privileges.

Try reading `/etc/shadow`:

```bash
cat /etc/shadow
```

A regular user should receive a permission error because `/etc/shadow` contains sensitive authentication information.

Now try:

```bash
sudo cat /etc/shadow
```

An authorized sudo user should be able to access it.

> **Key Concept:** Use elevated privileges only when they are actually required.

---

### Becoming Root Temporarily

If several administrative commands must be performed, you can start a root login shell:

```bash
sudo -i
```

Verify:

```bash
whoami
```

You should see:

```text
root
```

Return to your normal account with:

```bash
exit
```

Avoid remaining in a root shell longer than necessary.

---

### Changing Your Password

Use `passwd` to change your own password:

```bash
passwd
```

You will be prompted for your current password and then your new password.

An administrator can change another user's password with:

```bash
sudo passwd username
```

Use strong, unique passwords. For remote administration, SSH public-key authentication is generally preferable to password-only authentication.

---

### Changing the Hostname

View the current hostname:

```bash
hostnamectl
```

Change it with:

```bash
sudo hostnamectl set-hostname server01
```

Verify the change:

```bash
hostnamectl
```

The hostname identifies the system and is especially useful when administering multiple servers.

---

### Managing the Timezone

Check the current system time and timezone:

```bash
timedatectl
```

View available timezones:

```bash
timedatectl list-timezones
```

Set a timezone:

```bash
sudo timedatectl set-timezone America/New_York
```

Verify:

```bash
timedatectl
```

Timezone configuration is important because it can affect **logs, timestamps, and scheduled tasks**.

---

### Rebooting the System

A regular user may not have permission to reboot the system directly.

Administrative reboot:

```bash
sudo reboot
```

After reconnecting, verify that the server restarted:

```bash
uptime
```

A low uptime indicates that the system recently rebooted.

---

### Checking Login History

View previous logins:

```bash
last
```

Filter by a specific user:

```bash
last student
```

Check root login history:

```bash
last root
```

On systems that maintain the failed-login database, failed login attempts can be viewed with:

```bash
sudo lastb
```

---

### Reviewing `sudo` Activity

On systems using `systemd`, `sudo` activity may be available through the journal.

For example:

```bash
sudo journalctl _COMM=sudo
```

This can help administrators review when elevated privileges were used.

---

### Local vs. Global Changes

A **local change** generally affects only one user.

Examples include:

* Files inside the user's home directory
* User-specific shell settings
* User-specific environment variables

A **global change** affects the overall system or multiple users.

Examples include:

* Changing the hostname
* Installing software
* Managing services
* Changing system time settings
* Modifying system configuration files

Global changes commonly require `sudo`.

---

### Quick Reference

| Command                              | Purpose                                   |
| ------------------------------------ | ----------------------------------------- |
| `whoami`                             | Show the current user                     |
| `sudo <command>`                     | Run a command with elevated privileges    |
| `sudo -i`                            | Start a root login shell                  |
| `exit`                               | Leave the root shell                      |
| `passwd`                             | Change your password                      |
| `hostnamectl`                        | View hostname information                 |
| `sudo hostnamectl set-hostname NAME` | Change hostname                           |
| `timedatectl`                        | View time and timezone settings           |
| `timedatectl list-timezones`         | List available timezones                  |
| `sudo timedatectl set-timezone ZONE` | Change timezone                           |
| `sudo reboot`                        | Reboot the system                         |
| `uptime`                             | Show how long the system has been running |
| `last`                               | View login history                        |
| `sudo lastb`                         | View failed login attempts                |

---

### Quick Practice

```bash
# Identify your current user
whoami

# Check the hostname
hostnamectl

# Change the hostname
sudo hostnamectl set-hostname server01

# Verify
hostnamectl

# Check timezone
timedatectl

# List available timezones
timedatectl list-timezones

# Change timezone
sudo timedatectl set-timezone America/New_York

# Verify
timedatectl
```

### Key Takeaway

A Linux administrator should understand when elevated privileges are required without operating as `root` unnecessarily.

The basic pattern is:

```text
Regular user
     ↓
sudo <command>
     ↓
Administrative privilege
     ↓
Command completes
     ↓
Return to normal privileges
```

Use `sudo` deliberately, verify commands before executing them, and confirm system-level changes after they are made.
