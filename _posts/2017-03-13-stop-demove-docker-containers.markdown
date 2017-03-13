---
title:  "Stop and remove Docker containers"
date:   2017-03-13 18:00:00
description:
---

Quickest way to stop and remove your Docker containers all at once.

You're probably familiar that

```
$ docker ps
```

will list your containers. With

```
$ docker ps -q
```

you have only their container ids.

In this way, a simple way to stop your running containers is

```
$ docker stop $(docker ps -q)
```

You can also include in this list your already-exited containers by running

```
$ docker stop $(docker ps -qa)
```

In order to remove them, all you have to run is

```
$ docker rm $(docker ps -qa)
```

Cheers :)