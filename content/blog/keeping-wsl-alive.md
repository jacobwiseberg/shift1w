+++
date = '2026-02-08T09:39:56+01:00'
title = 'Keeping WSL Alive'
hn_thread_id = 47776781
+++

WSL is one of my favorite Windows tools, but it tends to shut itself down quicker than expected.

### Why should you keep WSL alive constantly?

My current laptop is an M1 MacBook Air that I received in 2021 in order to graduate college. It is a great machine and the never ending battery life continues to prevent me from looking for a new device. Meanwhile, the machine I've most recently acquired is a Beelink SER8 with 64 GB of RAM and 2 TB of storage. This device has a fantastic price to performance ratio and serves my every need, including open source development. It also provides my fiancée and I with a lovely "family" desktop that we share. Because of this, I am hesitant to make the hop to Linux as I want to keep the device as a safe space for backup storage and document processing that my fiancée can also utilize.

With this in mind, my answer to this first question is simple. I want a way to leverage my Fedora Linux terminal in a remote environment. This will turn my lovely M1 into a nice "Linux" development machine on the go. Keeping WSL alive is a key element of this setup. It will allow me to keep a mosh server up and running, ready to access connections from both my phone and my laptop.

### My development setup

To continue this mobile/stationary setup discussion, I will briefly run through the technologies I intend to use in my workflow. My goal is to leverage terminal applications. This includes:

- mosh: for stable connections
- NeoVim: for text editing
- tmux: for workspace management
- OpenCode: for AI

### 3 Layers of WSL modifications

1. The first layer is the changes in my .wslconfig. Most of these settings can also be accessed in the update WSL Settings app.

```ini
[wsl2]
memory=56294899712
vmIdleTimeout=-1
networkingMode=Mirrored
dnsTunneling=true
[experimental]
autoMemoryReclaim=Disabled
```

The key settings for keeping the VM alive are vmIdleTimeout and autoMemoryReclaim. The latter prevents further layers from being killed after long idle periods.

2. The second layer requires a custom program in the Startup folder in Windows. Easily accessible using Win+R then `shell:startup`. I call this file KeepWSLAlive.vbs:

```vb
Set WshShell = CreateObject("WScript.Shell")
' This runs the dbus-launch command which forces the WSL instance to stay active
' The 0 at the end tells Windows to run the command in a hidden window
WshShell.Run "wsl --exec dbus-launch true", 0, False
```

3. Finally, for my use case, I launch a mosh server instance.

This requires networkingMode=Mirrored, dnsTunneling=true. This allows my Tailscale on Windows to route packets correctly. It also requires an additional firewall rule set by: `New-NetFirewallRule -DisplayName "Allow Mosh UDP" -Direction Inbound -Protocol UDP -LocalPort 60000-60010 -Action Allow`.

#### A short thank you

If you made it to the end of this short post, thank you! I enjoy writing but have been struggling to get this blog up and running. A small post like this is exactly what I needed to push this site from the empty state it has been in!

*Disclaimer: while this Hugo site is maintained with the help of AI, no AI was used in the writing of this post.*