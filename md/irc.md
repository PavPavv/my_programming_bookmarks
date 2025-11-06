# My IRC (Internet Relay Chat) chat

## Pre-requirements for developing

1. Install IRC-client

```bash
$ sudo apt update && sudo apt install irssi
```

2. Run irssi

```bash
$ irssi
```

3. Save common Libera.chat server (skip)

```bash
$ /server add -auto -network libera irc.libera.chat 6667
```

4. Connect to Libera.chat server

```bash
/connect irc.libera.chat
```

5. Registration

```bash
/nick <your-nickname>
/msg NickServ REGISTER <your-password> <youremail@example.com> 
```

6. Then check email and run verification:

```bash
$ /msg NickServ VERIFY REGISTER <your-nickname> <uniqueHash>
```

7. Create my chat

```bash
$ /join #chat_name
```

8. Register my chat

```bash
/msg ChanServ REGISTER #chat_name
```

## Daily using

1. Start session

```bash
$ irssi
$ /connect irc.libera.chat
```

2. Confirm after every session start:

```bash
/msg NickServ IDENTIFY <your-password>
```

3. Join any chat

```bash
$ /join #chat_name
```