# Cheat sheet: tmux

Install tmux

```bash
sudo apt install tmux
```

Create new session

```bash
tmux new-session -s mySessionName
```

Split terminal vertically
> Ctrl+B + Shift+%

Split terminal horizontally
> Ctrl+B + Shift+"

Jump between terminals
> Ctrl+B Up/Down/Left/Right

Move panel right
> Ctrl+B + }

Move panel left
> Ctrl+B + {

Disconnect session
> Ctrl+B + d

Attach to existing session

```bash
tmux attach -t mySessionName
```
