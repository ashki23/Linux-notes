# Some configs for mac terminal 
*[Ashkan Mirzaee](https://ashki23.github.io/index.html) - November 2019*

### Zsh (or Bash) config
Open (create if not exist) `.zshrc` (or `.bash_profile` if using bash) file in home directory and add the following commands:

- Grep default color option: `alias grep='grep --color=auto'`
- Colored directories in `ls`: `alias ls='ls -G'`
- Git tab completion: `autoload -Uz compinit && compinit`

**Note:** we should logout and login to see the changes.

### Use Option as Meta key
To active this option, open `Terminal > Prefences` and select `Keyboard` tab and check `Use Option as Meta key`.

### Exit shell and close the window
To be able to close terminal window by `ctrl + d`, open `Terminal > Prefences` and select `Shell` tab and change `When the shell exits` to `Close the window`.

### Install Emacs
We can download Emacs from [here](https://emacsformacosx.com). Add the following line to the `.bash_profile` (or `.zshrc`) to activate `emacs` command in the terminal.

```bash
alias emacs='/Applications/Emacs.app/Contents/MacOS/Emacs -nw'
```

### Add Emacs config file `~/.emacs`:
```
;; Add MELPA
(package-initialize)
(add-to-list 'package-archives '("melpa" . "http://melpa.org/packages/") t)

;; Personal information
(setq user-full-name "Your Name"
      user-mail-address "your@email.com")

;; Backup in one place
(setq backup-directory-alist '(("." . "~/.emacs.d/backup")))

;; Turn on bracket match highlight
(show-paren-mode 1)
```

---
Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
