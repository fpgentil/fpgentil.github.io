---
title:  "Screen basics :)"
date:   2017-05-09 18:00:00
description:
---

"[Screen][screen] is a full-screen window manager that multiplexes a physical terminal between several processes"

Here are listed a few useful screen commands:

* Create a named session
```
$ screen -S NAME_OF_SESSION
```

* Detach an active session (inside)
```
C-a d
```

* Detach and logout an active session (inside)
```
C-a D D
```

* Detach a running session
```
screen -d NAME_OF_SESSION
```

* List sessions
```
$ screen -ls
```

This post tends to grow up! :)

[screen]: https://www.gnu.org/software/screen/manual/screen.html