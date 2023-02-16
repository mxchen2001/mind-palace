# Bash Snippets

Have your terminal show git branch name if you are in a git repo

```bash
parse_git_branch() {
	git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
```

Verbose `PS1` with git branch name

```bash
export PS1="\e[0;36m[\u@\h]\e[m \e[0;32m(\w)\e[m\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
```

Short `PS1` with git branch name

```bash
export PS1="\e[0;32m(\W)\e[m\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
```