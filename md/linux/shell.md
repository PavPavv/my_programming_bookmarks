# Bourne shell

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
