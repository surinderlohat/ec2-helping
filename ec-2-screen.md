Absolutely! Here are the common `screen` commands you’ll use on Linux to manage terminal sessions—super helpful when running apps like Next.js or your Python API on EC2 and you want them to keep running after you disconnect.

---

# `screen` Commands Cheat Sheet

### Start a new screen session

```bash
screen -S session_name
```

* Creates a new screen session named `session_name`.
* If you don’t provide `-S session_name`, it creates a session with a default numeric ID.

---

### Detach from current screen session (keep it running in background)

* Press:
  `Ctrl + a` then `d`
* This detaches you from the session and brings you back to the normal shell prompt.

---

### List all existing screen sessions

```bash
screen -ls
```

Example output:

```
There is a screen on:
    1234.session_name   (Detached)
1 Socket in /var/run/screen/S-user.
```

---

### Reattach to a detached screen session

```bash
screen -r session_name
```

or if you have multiple sessions, use the session ID:

```bash
screen -r 1234
```

---

### Reattach forcibly if session is attached elsewhere

```bash
screen -D -r session_name
```

---

### Kill a screen session

1. Reattach to it:

```bash
screen -r session_name
```

2. Inside the session, type:

```bash
exit
```

or press `Ctrl + d` to terminate it.

Or kill by ID:

```bash
screen -X -S session_name quit
```

---

### Useful inside screen

* `Ctrl + a` then `c` — Create a new window inside screen
* `Ctrl + a` then `n` — Switch to next window
* `Ctrl + a` then `p` — Switch to previous window
* `Ctrl + a` then `k` — Kill current window
* `Ctrl + a` then `?` — Show help screen for commands

---

If you want, I can also help with `tmux` commands — an alternative to `screen` that’s quite popular.
