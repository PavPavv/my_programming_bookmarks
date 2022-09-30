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
