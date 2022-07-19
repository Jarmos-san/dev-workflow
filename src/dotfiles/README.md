# Managing my Personal Dotfiles

On Linux-based machines, its not uncommon to stumble across many software
relying on configuration files where the names usually start with a _period_
(`.`). Examples of such popular configuration files are `.vimrc`, `.gitignore` &
so on. The caveat is, on Linux-based OSes **ANY** filenames starting with a
period is considered a hidden file (_how convenient right?_)! You can read more
about these files at - [GitHub Does Dotfiles][1]

That said, today filenames do not necessarily have to start with a period but
the standard has stuck through history. So, the next time you see someone
mention checking out their "_dotfiles_" repository, they're probably asking you
to see how they configure their tools of choice!

A bit of a shameless plug though 😛 feel free to checkout [my personal dotfiles
repository][2] as well!

Backing up my personal dotfiles is only half the task, managing & copying them
across different machines I use on a day-to-day basis is where the difficult
tasks comes into light. But thanks to [`chezmoi`][3] managing my dotfiles is
easier than ever!

We'll discuss more about the tool in the next chapter but for now here's a
summary of what the tool does:

1. Provides an intuitive CLI-based UI/UX which means no more complicated Bash
   scripts!
2. It automates (as much as it can) functionalities like cloning, remote
   backups, editing the dotfiles & so on with much ease.

The tool is written in [Golang][4] which means its fast & easy to install as a
single binary across all of my machines! I don't need to rely on [`stow`][5]
and/or PowerShell scripts anymore! If that piqued your interest in
using/checking out `chezmoi` then go ahead & check out the next chapter where I
discuss how I use the tool in more details.

<!-- References: -->

[1]: http://dotfiles.github.io
[2]: https://github.com/Jarmos-san/dotfiles
[3]: https://chezmoi.io
[4]: https://go.dev
[5]: https://www.gnu.org/software/stow
