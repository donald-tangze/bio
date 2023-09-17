The Bourne Again Shell, or **[Bash](https://www.gnu.org/software/bash/manual/bash.html)**, is a [Unix](https://www.codecademy.com/resources/docs/general/unix)-based shell program and language used for a multitude of purposes including system administration and software testing.

Developed by Brian Fox in 1989, Bash was released as part of the GNU Project to replace the original Bourne Shell. It was also one of the first programs ported to [Linux](https://www.codecademy.com/resources/docs/open-source/linux).

## Operating System Compatibility

Over time, Bash has become available across many operating systems both as a default shell or an installable program.

### Linux

Due to their mutual relationship with the GNU Project, Bash is the default shell on most distributions of Linux such as the following:

- [CentOS](https://www.centos.org/)
- [Debian](https://www.debian.org/)
- [Ubuntu](https://ubuntu.com/)

### macOS

Apple macOS featured Bash as the default from 2003 with OS X Panther (version 10.3), to 2019 with Catalina (version 10.15). Since then, Z shell (or `zsh`) is the default shell for macOS.

> **Note:** Bash can still be used as an alternative in newer versions of macOS. The switch can be made by:
>
> 1. Running `chsh -s bin/bash` in the Terminal window.
> 2. Confirming the change with the user’s credentials.
> 3. Closing and reopening the Terminal window.

don2021@Mac31 /bin % sh -version
GNU bash, version 3.2.57(1)-release (arm64-apple-darwin22)
Copyright (C) 2007 Free Software Foundation, Inc.

zsh 5.9 (x86_64-apple-darwin22.0)



don2021@Mac31 ~ % echo $0
-zsh

[Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/index.html)