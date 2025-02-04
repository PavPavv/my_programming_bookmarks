# Bourne again shell

## Shebang

```bash
#!bin/sh
```

Means that file should be interpreted by unix program located at /bin/sh

## Basics

### Envs, operators, conditions

**bash** run bush script

```bash
bash test.sh
```

**echo** print next strings after space

```bash
#!bin/sh

echo Print something!
```

**printf** formatted output

```bash
#!/bin/bash

test='TEST'

printf "hello, $test"
```

**''** single quotes - pure string literal
**""** double quotes - strings with templates

**${argNum}** command argument

**$#** arguments amount

**shift** shift and remove argument

**$@** all arguments

**$0** script name

**$$** PID

**$?** exit code

```bash
#!/bin/sh
if [ "$1" = "hi" ] || [ "$1" = "wazzup" ]
then
  echo 'The first argument was "hi"'
elif [ "$2" = "buy" ]
then
  echo 'The second argument was "bye"'
else
  echo -n 'The first argument was not "hi" -- '
  echo It was '"'$1'"'
fi
```

**=** equality operator

**!=** not equals operator

**||** or operator

**&&** and operator

### Loops

```bash
#!/bin/sh
for str in one two three four
do
  echo $str
done
```

### Scripts

#### Run script, execute script

```bash
chmod +rx scriptname # read/exe for anybody
```

```bash
chmod u+rx scriptname # read/exe only for file's owner
```

### Redirections

Before a command is executed, its input and output may be redirected using a special notation interpreted by the shell. Redirection allows commands’ file handles to be duplicated, opened, closed, made to refer to different files, and can change the files the command reads from and writes to. Redirection may also be used to modify file handles in the current shell execution environment. The following redirection operators may precede or appear anywhere within a simple command or may follow a command. Redirections are processed in the order they appear, from left to right.
