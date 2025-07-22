# CLI (Command Line Interface)

A quick reference for essential command line operations on Linux, macOS, and Windows (with Git Bash).

---

## Navigation & Information

| Command             | Description                |
|---------------------|---------------------------|
| `pwd`               | Print working directory   |
| `ls`                | List files in directory   |
| `ls -l`             | List with details         |
| `ls -a`             | List all (including . files)|
| `cd folder`         | Change directory          |
| `cd ..`             | Up one directory          |
| `cd ~`              | Go to home directory      |
| `tree`              | Display directory tree    |

---

## File & Folder Manipulation

| Command             | Description                |
|---------------------|---------------------------|
| `touch file.txt`    | Create empty file          |
| `mkdir folder`      | Create new folder          |
| `rm file.txt`       | Remove file                |
| `rm -r folder`      | Remove folder recursively  |
| `cp src dest`       | Copy file/folder           |
| `mv src dest`       | Move or rename             |
| `cat file.txt`      | View file contents         |
| `head file.txt`     | First 10 lines of file     |
| `tail file.txt`     | Last 10 lines of file      |
| `less file.txt`     | Scroll file contents       |
| `echo "text"`       | Print text                 |

---

## Searching

| Command                       | Description                      |
|-------------------------------|-----------------------------------|
| `grep "pattern" file.txt`     | Search for pattern in file        |
| `grep -r "pattern" folder/`   | Recursive search in folder        |
| `find . -name "*.js"`         | Find files matching name          |
| `which command`               | Show command location             |
| `locate filename`             | Find file by name (uses database) |

---

## Permissions

| Command                 | Description                           |
|-------------------------|---------------------------------------|
| `chmod 644 file.txt`    | Change file permissions               |
| `chmod +x script.sh`    | Make file executable                  |
| `chown user:group file` | Change file owner/group               |

---

## Process Management

| Command           | Description                       |
|-------------------|-----------------------------------|
| `ps aux`          | List all running processes        |
| `top`             | Display real-time system stats    |
| `htop`            | Interactive process viewer        |
| `kill PID`        | Kill process by PID               |
| `pkill name`      | Kill process by name              |

---

## Networking

| Command                       | Description                        |
|-------------------------------|------------------------------------|
| `ping example.com`            | Test network connection            |
| `curl http://example.com`     | Fetch web page (show source)       |
| `wget http://example.com`     | Download file/web page             |
| `ssh user@host`               | Connect to remote host via SSH     |
| `scp file user@host:/path`    | Secure copy file to remote host    |

---

## Archiving & Compression

| Command                       | Description                        |
|-------------------------------|------------------------------------|
| `tar -cvf archive.tar folder` | Create tar archive                 |
| `tar -xvf archive.tar`        | Extract tar archive                |
| `tar -czvf archive.tar.gz folder` | Create gzip compressed archive  |
| `tar -xzvf archive.tar.gz`    | Extract gzip compressed archive    |
| `zip archive.zip file`        | Create zip archive                 |
| `unzip archive.zip`           | Extract zip archive                |

---

## Package Managers

| Command                     | Description                        |
|-----------------------------|------------------------------------|
| `apt update`                | Update package list (Debian/Ubuntu)|
| `apt install packagename`   | Install package (Debian/Ubuntu)    |
| `yum install packagename`   | Install package (RHEL/CentOS)      |
| `brew install packagename`  | Install package (macOS/Homebrew)   |
| `npm install package`       | Install Node.js package            |
| `yarn add package`          | Install package with Yarn          |

---

## Miscellaneous

| Command           | Description                       |
|-------------------|-----------------------------------|
| `history`         | Show command history              |
| `clear`           | Clear terminal screen             |
| `man command`     | Show manual for command           |
| `date`            | Display current date/time         |
| `whoami`          | Show current user                 |
| `df -h`           | Show disk space usage             |
| `du -sh folder`   | Show size of folder               |

---

## Sudo and Superuser

| Command           | Description                       |
|-------------------|-----------------------------------|
| `sudo command`    | Run command as superuser          |
| `su user`         | Switch to another user            |

---

## Tips

- Use **Tab** for autocompletion.
- Use **Ctrl+C** to cancel a running command.
- Use **Ctrl+R** to search command history.
- Use **Up/Down arrows** to browse previous commands.

---

> **Note:** Some commands may vary or require installation on Windows (use Git Bash, WSL, or PowerShell equivalents).