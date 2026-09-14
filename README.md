# My Linux Upskill Challenge Journal
BITA Kernel Crew · Cohort 1 · Sept 2026

## Day 0
- Digital Ocean VPS Set-up
    - This option for me was just out of curiosity from using a new tool product, as I have spent years learning on the most cheapest and effective VM out there which is Virtual Box aka my Go To for Labbing.
    
- Problems I hit and how I fixed them:
None so far. These are all refresher commands for me. I am not a System Admin so alot of these commands, while I have general knowledge of....they arent ones that I utilize to get my job (cloud engineer), none the less Give me all the Linux tools to the kingdom. Im here for it!


## Day 1 - Get to know your server
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

## Day 2 - Basic Navigation
This is my jam! Honestly this is how I have survived using Linux and is absolutely the foundation to understanding and using the command line intentionally.

### Commands
- man - will be your bestfriend...use it! executing man along with a command will give you the manual on the command that you want to know more about.
- pwd - Print working directory. This will let you know where you are currently in the system. it will show your absolute path.

...... will finish later
