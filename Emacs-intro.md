# Emacs: a powerfull text editor
A good text editor could provide an environment to write and edits codes easier. Many would like to use IDEs to write and run  codes, that might be very useful for small programs, but as long as your projects being larger wiriting and editing codes become a very tedius task. [Emacs](https://www.gnu.org/software/emacs/) is one of the best editors that could be very helpful to work on the text faster and easier. It might be very challenging to start using any editors like Emacs, but it is definitely worth to spend some time to learn the first steps. This tutorial provides a list of commands and configurations that you might need to begin.

## Config file
Use a text editor to create Emacs config file called `.emacs` in the home directory `cd ~` then insert the following to make your very preliminary configurations by:
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

;; Auto insert closing bracket
(electric-pair-mode 1)
```

## Commands
To strat working Emacs you might need to install it first. To install Emacs follow the instraction at [GNU Emacs](https://www.gnu.org/software/emacs/download.html). Briefly for:
- Linux (Debian) use `sudo apt install emacs`
- Mac use [binaries](https://emacsformacosx.com/) - see config [here](https://github.com/ashki23/Linux-notes/blob/master/Mac_terminal.md)

The following are some important commands in Emacs. Note that **`C-`** means **`ctrl`** and **`M-`** means **`alt`**.

- `C-x C-c`: exit
- `C-z`: suspend
- `C-k`: kill the line
- `C-w`: cut the line/text 
- `M-w`: copy the line/text
- `C-y`: uncut/paste the line/text (yank)
- `C-space arrow keys`: select text
- `C-shift arrow keys`: select paragraphs
- `C-x u`: undo
- `C-a`: move to the beginning of the line
- `C-e`: move to the end of the line
- `C-home`: move to the beginning of the buffer
- `C-end`: move to the end of the buffer
- `M-g g`: go to line
- `C-s`/`C-r`: search/reverse search
- `M-%`: replace
- `C-g`: stop a command
- `C-x C-f`: make/open a file as a new buffer
- `C-x b`: change the buffer
- `C-x k`: kill the buffer
- `C-x 1`: close other windows
- `C-x 0`/`q`: close/quit windows
- `C-x o`: switch to other windows
- `C-h ?`: help list
- `C-h t`: tutorial 
- `C-h d`: search help for a pattern
- `C-h c`: show help for the command
- `M-x <command>`: run commands
- `M-x ispell`: spell check; enter the suggested `digit` or `a` to accept or `r` to rewrite
- `M-x package-install`: install packages 
- `M-x package-list-packages`: list of packages

You may find more details in:
- [7 Basic Editing Commands](https://www.gnu.org/software/emacs/manual/html_node/emacs/Basic.html#Basic)
- [Emacs manual](https://www.gnu.org/software/emacs/manual/html_node/emacs/index.html)

## Customize faces
An easy way to change the appearance of Emacs is changing faces. `M-x list-faces-display` shows all of the faces that currently defined and you may modify them (use GUI Emacs to access them by clicking). To customize certain faces, use `M-x customize-face` and select the face that you wnat to change (press tab to see all options).

Also, you are able to customize faces from Emacs config file. For instance by adding following to `.emacs` file you will change some faces in the Emacs terminal mode:
```
;; Customize faces
(custom-set-faces
 '(font-lock-builtin-face ((t (:foreground "SkyBlue1"))))
 '(font-lock-comment-delimiter-face ((t (:foreground "salmon"))))
 '(font-lock-comment-face ((t (:foreground "chocolate1" :slant oblique))))
 '(font-lock-constant-face ((t (:foreground "lime green"))))
 '(font-lock-doc-face ((t (:foreground "light coral" :slant oblique))))
 '(font-lock-function-name-face ((t (:foreground "green" :weight bold))))
 '(font-lock-keyword-face ((t (:foreground "SteelBlue1" :weight bold))))
 '(font-lock-preprocessor-face ((t (:foreground "cornflower blue" :slant italic))))
 '(font-lock-regexp-grouping-backslash ((t (:weight bold))))
 '(font-lock-regexp-grouping-construct ((t (:weight bold))))
 '(font-lock-string-face ((t (:foreground "violet" :slant italic))))
 '(font-lock-type-face ((t (:foreground "green" :weight bold))))
 '(font-lock-variable-name-face ((t (:foreground "lime green"))))
 '(font-lock-warning-face ((t (:foreground "dark orange" :weight bold))))
 '(minibuffer-prompt ((t (:foreground "lime green" :weight bold)))))
 ```

To change the theme use `M-x load-theme`, then press `tab` to show a list of available themes. To clear theme use `M-x disable-theme`.

## Install packages
In Emacs you can install extra packages based on your needs. To install a new package, press `M-x` and type `package-refresh-contents` to fetch all packages and then use `M-x package-install` and enter the new package's name. For example you can install Markdown-mode, htmlize and ESS (R-mode) packages with:
```
M-x package-install markdown-mode
M-x package-install htmlize
M-x package-install ess
```
To see list of the available packages use `M-x package-list-packages`. And to delete packages, use `M-x package-delete` and enter the package's name. Note that you may use `C-s`/`C-r` for searching and  `C-g` to cancel any actions and `q` to close buffers in Emacs. 

