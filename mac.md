# list installed brew packages in a tree

```
installed_packages=$(brew list --formula | sed "s/^/ /; s/$/$/")
for package in $(brew leaves)
    brew deps --tree --formula $package | grep -E "$installed_packages|^$package$|^$"
```

# terminal profile ~/.zshrc

```
setopt PROMPT_SUBST

gitbranch() {
    local message
    message=$(git branch 2>&1 | grep "^* " | sed "s/^* / %F{purple}on%f %F{green}%B/" | sed "s/$/%b%f/" | sed "s/^ %F{purple}on%f %F{green}%B(/ %F{purple}with%f %F{yellow}%B/" | sed "s/)%b%f$/%b%f/")
    echo $message
}

PS1=$'\n''%F{red}%B%n%b%f %F{purple}on%f %F{blue}%B%m%b%f %F{purple}in%f %F{magenta}%B%2~%b%f$(gitbranch)'$'\n''    %% '

preexec() {
    echo
}
```


