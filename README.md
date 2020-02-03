![Setup](./media/setup.png)

# My Dotfiles 

This repository is my current `dotfiles` setup. 

* `.aliases` - some useful shortcuts to do common stuff faster;
* `.zprofile` - useful fuctions and some shell configurations;
* `.zshrc` - loading of `.aliases`, `.zprofile` and all dependencies.

## ToC

- [Examples](#examples)
    - `.aliases`
    - `.zprofile`
- [Install](#install)


## Examples 

Some examples. To learn more, please, look into files itself 😇

### `.aliases`

```bash
# Open GitHub repo for current direcroty
alias gho='open https://github.$(git config remote.origin.url | cut -f2 -d. | tr ':' /)'
```

### `.zprofile`

```shell
# Creates directory and git repository from currently opened GitHub repo in Safari	
ghi() {
    url=$(osascript -e 'tell application "Safari" to return URL of front document')
    if is_git_remote_url_reachable "$url"; then
        dir_name=${url##*/}
        cd ~/Downloads
        mkdir $dir_name
        cd $dir_name
        git init
        echo "# $dir_name" >> README.md
        git add README.md
        git commit -m "Init ✨"
        git remote add origin $url
        git push -u origin master
    else
        echo -e "\e[31mBAD URL\e[0m"
    fi
}

# Move to trash instead of instant delete 
t() {
    if [[ -n "$1" ]]; then
        mv $@ ~/.Trash
    else
        echo -e "\e[31m!ERROR!\e[0m At least one file/directory name should be passed"
    fi
}
```

## Install

⚠️ **Important**

1. You should use `zsh`
2. Clone this repo into `~/.dotfiles`
3. Create link to `.zshrc` in `~/` with next command `ln -s ~/.dotfiles/.zshrc ~/.zshrc` 
4. ✅