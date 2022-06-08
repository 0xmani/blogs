---
title: "Stabilizing the Dump Shell"
date: 2022-06-07T23:38:30-07:00
draft: false
tags: ["Reverse Shell", "privilege", "python", "shell", "CTF"]
categories: ["Pentesting", "CTF"]
author: "Manikandan"
comment: true
---

Hello All, This is my first blog that explains how to stabilize the shell in Linux.

While playing CTF Challenges, it is often to spawn a reverse shell on the target machine. Other than ssh shell, every shell is a dump which often kills the reverse shell and this shell doesn't give you the proper shell functionalities like tab completion, "su" command, clear the terminal, etc. Sometimes, pressing "ctrl+c" completely kills your reverse shell.

Shell Stabilization prevents you from killing your reverse shells and adds proper shell functionalities.

Note: This post assumes you already a reverse shell on the target machine.

To upgrade a TTY dump shells

**Python3**
```bash
python3 -c "import pty; pty.spawn('/bin/bash)"
(or)
python -c "import pty; pty.spawn('/bin/bash)"
``` 

**Bash**
```bash
/usr/bin/script -qc /bin/bash /dev/null
(or)
/bin/sh -i
```

**Perl**
```bash
perl —e 'exec "/bin/sh";'
(or)
perl: exec "/bin/sh";
```

**Ruby**
```bash
ruby: exec "/bin/sh"
```

**lua**
```bash
lua: os.execute('/bin/sh')
```

Then press ctrl+z to background the process.

Run the following command in attacker machine, 

**Attacker Machine**
```bash
stty raw -echo
fg
ENTER
ENTER
```
Run "stty raw -echo" and "fg" command on the attacker machine, then click double ENTER. The reverse shell will be retrieved.

**Victim Machine**
```bash
export TERM=xterm
stty cols 132 rows 34
```
Set the terminal environment to variable (e.g. xterm, xterm-256, etc)

All Done!. Now you should have a stabilized bash shell that can tab complete, clear the screen, and use Ctrl+C.

