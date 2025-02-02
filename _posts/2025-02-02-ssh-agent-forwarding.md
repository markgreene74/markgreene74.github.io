---
layout: post
title:  "SSH agent forwarding"
categories: ssh remote-dev
author: markgreene74
---

I have a small local VM (virtual machine) for remote development. A `devcontainer` will not work in this case, so I am stuck with a VM.

Now, I may need to use `git` to pull a repo on the VM and eventually push some changes but at the same time I really don't want to generate a new set of `ssh` keys, add them to GH, etc.

The solution: use SSH agent forwarding ([link to the GitHub docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding)).

- open the appropriate `ssh` config, in my case `~/.ssh/vscode.config` as I am going to use the remote dev features of VSCode for this project
- add `ForwardAgent` like in this example
    ```
    Host debian-local
        HostName <IP address>
        User <username>
        ServerAliveInterval 120
        ForwardAgent yes
    ```
- test that everything is working in the terminal
    ```
    username@debian-test:~/monitoring-stack$ ssh -T git@github.com
    Hi markgreene74! You've successfully authenticated, but GitHub does not provide shell access.
    ```
