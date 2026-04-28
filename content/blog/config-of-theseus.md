+++
date = '2026-04-15T17:13:54+02:00'
title = 'My .config Ship of Theseus'
hn_thread_id = 47886157
+++

Micromanaging my .config folder has allowed me to create a simple and effective install file so I can pull my setup into a new machine instantly, and modify my environment intentionally.

### My previous method of TUI exploitation

I have dabbled with tmux and neovim on and off over the years. While I have yet to integrate it into my professional workflow, I do enjoy the slow development process for my personal projects (espcially in this hypersonic AI era). One of my fondest memories when I was first diving into code was making my terminal interface look cool, through projects like Oh My Zsh and dual booting linux distros on my tiny Lenovo Yoga I routinely pushed to the limits for my robotics team. I always made sure to back up my config files onto Github. This allowed me to get familiar with git early and have a better overview of the filesystems I was working with. This process was always fragmented and I regularly scrapped my work for something completely new. The result was three repositories, one for tmux, one for neovim, and one for zsh. All managed seperately, all disposable whenever I got bored.

### My reaction to the AI developer "renaissance"

While I feel less threatened than I did initially, I generally run as a more anxious personality and try to keep up with all the new tools. Like many others, this has allowed me to spot patterns and convergence with the direction of the AI developer experience. My goal here is to make strides to leverage it in my own future-proof way. I have used VS Code pretty consistently since it replaced Atom as the best tool to get the job done. I have downloaded and tried out Cursor, Zed, Antigravity, and countless other spinoffs with their own flavor of AI integration.

Eventually, I switched my perspective towards seeing compute as a commodity. I (like many others) landed on wanting a solution that didn't lock me into one LLM provider. Many of these systems allow provider switching, but I wanted something that couldn't be locked down at some future date. This drove me back into neovim, and more importantly, OpenCode. Again, I scrapped all previous configurations, spun up my terminal environment, and committed to locking down a sustainable and intentional workflow for myself.

### Using gitignore as a guardrail

Rather than pushing my entire nvim or tmux folder (located within my .config folder). I tried to zoom out and clear away anything that I didn't have direct control over. This meant stripping these directories down to what I control, and building from there. The heart of this became my .gitignore file. I took a whitelisting approach to micromanage every file that truly needs to be modified. While there might be some redundancies, this is what I landed on:

```bash
# Ignore everything
*

# Allow the directories themselves
!*/

# Allow the root-level files
!.gitignore
!new-terminal.sh

# Whitelist config files
!/zsh/.zshrc
!/tmux/tmux.conf
!/nvim/**
!README.md

# Blacklist the junk folders
/zsh/.oh-my-zsh/
/zsh/custom/plugins/*
/zsh/.zsh_history
/zsh/.zcompdump*
/nvim/doc/tags
**/tmux/plugins/**/.gitignore
**/zsh/custom/plugins/**/.gitignore
/nvim/.gitignore
/tmux/plugins/*
/zsh/custom/plugins/*
/tmux/plugins/*
*.log
*.swp
.DS_Store
```

Ideally, this prevents me from adding unecessary things and forces me to think about only what is strictly needed to maintain my setup.

### Intentionally spending more time in the terminal

The terminal is a fantastic, distraction free environment. Things only get displayed if the user chooses them to be displayed. While AI moves people further from the code they write, a terminal interface can bring someone closer. Building my new config has allowed me to tinker with OpenCode while feeling in touch with each line that gets written. I am no expert, and my current setup is admittedly slower for me than IntelliJ and VS Code (what I use at my day job). But maybe someday this workflow will become faster and then I can bring it into my professional environment. When that day happens, I'll be overpreppared with an install script and everything.

If you are interested, you can try it by running ``curl -fsSL https://shift1w.com/assets/new-terminal.sh | bash``. Since this a hyperpersonalized experience, it will probably break. It took a lot of old-school experimentation for me to get an output I am happy with on my machines. Though, if you are really interested, I would point you to the [repository](https://github.com/jacobwiseberg/.config). I have a README that should help with setup.

Through the chaos of AI and a personal ongoing professional transition, I have really enjoyed revamping my configurations for the programs I love using. It brought my closer to the code I write while allowing me to get more familiar using AI at a level I can feel comfortable scaling. I hope to build a long career and getting close with the tools is a fantastic way to improve in a fun and semi-productive manner.