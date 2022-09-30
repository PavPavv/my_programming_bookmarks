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

Install software package

```bash
sudo apt install nameOfProgram
```

Check OS version

```bash
lsb_release -a
```

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

Copy files

```bash
cp name.file copiedName.file
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

Create file

```bash
touch index.ts
```

Replace file

```bash
mv test/some.txt ../docs/test
```

Remove file

```bash
rm file.exe
```

Copy all files in directory

```bash
rm testDir/*
```

Remove entire folder

```bash
rm -rf someDir
```

Read text file

```bash
cat text.txt
```

Read pdf file

```bash
evince text.pdf
```

Turn off system

```bash
sudo shutdown -h now
```

Turn off system

```bash
sudo shutdown -h now
```

Unzip archive

```bash
tar -xvf archName
```

Unrar rar-archive

```bash
unrar e file.rar
```

Edit hosts file

```bash
sudo gedit /etc/hosts
```

Get user's rights back

```bash
sudo chown -R $USER:$USER .
```

Get user's rights back

```bash
sudo chown -R some/path
```

> systemd is an init system and system manager  and systemctl command is the central management tool for controlling the init system. In systemd, the target of most actions are “units”, which are resources that systemd knows how to manage. For service management tasks, the target unit will be service units, which have unit files with a suffix of .service. However, for most service management commands, you can actually leave off the .service suffix, as systemd is smart enough to know that you probably want to operate on a service when using service management commands.

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
