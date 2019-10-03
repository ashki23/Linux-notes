# Some configs for mac terminal 

### Grep default color option
```bash
alias grep='grep --color=auto'
```

### Colored directories in `ls`:
```bash
alias ls='ls -G'
```

**Note:** To be able to keep above changes, you need to open (create if not exist) `.bash_profile` file and add the above commands in that file. You should logout and login to see the changes.

### Add Emacs config file `~/.emacs`:
```bash
;; Personal information
(setq user-full-name "Ashkan Mirzaee"
      user-mail-address "ashkan.m23@gmail.com")

;; Backup in one place
(setq backup-directory-alist '(("." . "~/.emacs.d/backup")))

;; Turn on bracket match highlight
(show-paren-mode 1)
```
