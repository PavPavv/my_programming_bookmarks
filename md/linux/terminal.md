# Cheat sheet: linux terminal

> apt-get is an outdated linux package manager. apt (Advanced Package Tool) is new package manager. Also there are a snap, dpkg tools to install packages of software.

- [Ubuntu snap vs. apt: Which package manager to use and when](https://www.techtarget.com/searchitoperations/tip/Ubuntu-snap-vs-apt-Which-package-manager-to-use-and-when)

Open terminal with keyboard

> Ctrl+Alt+T

Copy from terminal

> Ctrl+Shift+C

Paste in terminal

> Ctrl+Shift+V

Abort of program in terminal

> Ctrl+C

## Basic

Get system user name

```bash
whoami
```

Get current path

```bash
pwd
```

Clear terminal

```bash
clear
```

Exit terminal

```bash
exit
```

## Install

Install software package

```bash
sudo apt install nameOfProgram
```

Check OS version

## Check system

```bash
lsb_release -a
```

## Disks

Check free space

```bash
df -h
```

## Directories

Enter directory

```bash
cd
```

Enter root directory

```bash
cd ~
```

Table of content of the current folder

```bash
ls
```

Table of content of the current directory

```bash
ls -la
```

Copy folder

```bash
cp -v
```

Rename folder

```bash
mv oldNameFolder newNameFolder
```

Create directory

```bash
mkdir
```

Remove entire folder

```bash
rm -rf someDir
```

## Files

Create file

```bash
touch index.ts
```

Replace file

```bash
mv test/some.txt ../docs/test
```

Copy files

```bash
cp name.file copiedName.file
```

Remove file

```bash
rm file.exe
```

Copy all files in directory

```bash
rm testDir/*
```

Read text file

```bash
cat text.txt
```

Read pdf file

```bash
evince text.pdf
```

Find regEx pattern in certain file or files

```bash
grep rx package.json
```

```bash
grep rx ./*
```

Find regEx pattern in certain file or files case insensitive

```bash
grep -i rx package.json
```

Find all not regEx pattern in certain file or files

```bash
grep -v rx package.json
```

### File access rights (change mode)

```bash
chmod go+r <file-name>
```

644, 600 (files)- 755, 700, 711 (directories, programs)

#### File being executed only by its name

1. Write a script with a shebang:

```bash
#!/usr/bin/env python3
```

2. Make the Script Executable:

    2.1 To run your script by just typing my_app, you need to move it to a directory that is included in your system's PATH. A common choice is /usr/local/bin or you can create a custom directory for your scripts.

    2.2 In Linux (including Ubuntu), the PATH is an environment variable that specifies a set of directories where executable programs are located. When you type a command in the terminal, the shell searches through these directories in the order they are listed in the PATH variable to find the corresponding executable file.

```bash
chmod +x my_app.py   
```

3. Move the Script to a Directory in Your PATH:

```bash
sudo mv my_app.py /usr/local/bin/my_app
```

## Manipulate system

Turn off system

```bash
sudo shutdown -h now
```

Turn off system

```bash
sudo shutdown -h now
```

## Archives

Unzip archive

```bash
tar -xvf archName
```

Unrar rar-archive

```bash
unrar e file.rar
```

## Network

Edit hosts file

```bash
sudo gedit /etc/hosts
```

Check 3000 port for processes

```bash
sudo netstat -tulpn | grep :3000
```

Kill process at the port of 3000

```bash
sudo fuser -k 3000/tcp
```

## User

Get user's rights back

```bash
sudo chown -R $USER:$USER .
```

Get user's rights back

```bash
sudo chown -R some/path
```

## Processes

Processes list, managing processes

```bash
ps
```

Processes list running by user

```bash
ps x
```

All the running processes

```bash
ps ax
```

All the running processes with full command names

```bash
ps w
```

Kill the process by its id (like Ctrl+D ?)

```bash
kill <pid>
```

Freeze the process by its id

```bash
kill -STOP <pid>
```

Continue previously freezed process by its id

```bash
kill -CONT <pid>
```

Interrupt previously freezed process by its id (like Ctrl+C)

```bash
kill -INT <pid>
```

Totally destroy process in CPU's memory by its id (only rare emergency cases)

```bash
kill -KILL <pid>
```

```bash
kill -9 <pid>
```

> systemd is an init system and system manager and systemctl command is the central management tool for controlling the init system. In systemd, the target of most actions are “units”, which are resources that systemd knows how to manage. For service management tasks, the target unit will be service units, which have unit files with a suffix of .service. However, for most service management commands, you can actually leave off the .service suffix, as systemd is smart enough to know that you probably want to operate on a service when using service management commands.

Start service

```bash
sudo systemctl start application.service
```

```bash
sudo systemctl start application
```

Stop service

```bash
sudo systemctl stop application.service
```

Restart service

```bash
sudo systemctl restart application.service
```

Reload service

```bash
sudo systemctl reload application.service
```

Reload or restart service

```bash
sudo systemctl reload-or-restart application.service
```

Enable service

```bash
sudo systemctl enable application.service
```

Disable service

```bash
sudo systemctl disable application.service
```

Checking the status of service

```bash
sudo systemctl status application.service
```

Check if service is enable

```bash
sudo systemctl is-enabled application.service
```

Check if service is failed

```bash
sudo systemctl is-failed application.service
```

To see a list of all of the active units that systemd knows about, we can use the list-units command:

```bash
sudo systemctl list-units
```

To see a list of all of the active and non-active units too

```bash
sudo systemctl list-units --all
```

```bash
sudo systemctl list-units --all --state=inactive
```

```bash
sudo systemctl list-units --type=service
```
