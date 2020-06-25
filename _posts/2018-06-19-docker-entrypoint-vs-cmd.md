---
title: "Docker ENTRYPOINT VS CMD"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Docker
---

# CMD vs ENTRYPOINT
<!-- TOC -->

- [CMD vs ENTRYPOINT](#cmd-vs-entrypoint)
  - [Override](#override)
  - [Shell vs. Exec](#shell-vs-exec)
  - [ENTRYPOINT and CMD](#entrypoint-and-cmd)
  - [Always Exec](#always-exec)

<!-- /TOC -->

Both ENTRYPOINT and CMD allow you to specify the startup command for an image,
but there are subtle differences between them. There are many times where 
you'll want to choose one or the other, but they can also be used together.

## Override
The ENTRYPOINT or CMD that you specify in your Dockerfile identify the default
executable for your image. However, the user has the option to override either
of these values at run time.

The recommendation is use CMD in your Dockerfile when you want the user of your
image to have the flexibility to run whichever executable they choose when 
starting the container.

In contrast, ENTRYPOINT should be used in scenarios where you want the container
to behave exclusively as if it were the executable it's wrapping.

## Shell vs. Exec
Both the ENTRYPOINT and CMD instructions support two different forms: the shell 
form and the exec form.

* Shell form: `CMD executable param1 param2`
* Exec form: `CMD ["executable","param1","param2"]`

Shell form always start a shell to execute the command.

Whether you're using ENTRYPOINT or CMD (or both) the recommendation is to 
**always use the exec form**s so that's it's obvious which command is running
as PID 1 inside your container.


## ENTRYPOINT and CMD
Combining ENTRYPOINT and CMD allows you to specify the default executable for 
your image while also providing default arguments to that executable which may 
be overridden by the user.
CMD will be treated as parameters of ENTRYPOINT
```
FROM ubuntu:trusty
ENTRYPOINT ["/bin/ping","-c","3"]
CMD ["localhost"]
```

`docker build -t ping .`

You can run `docker run ping google.ca` to override cmd, then the command in 
docker will be `/bin/ping -c 3 google.ca`
