# Emacs config

In the home directory `cd ~`, use `nano .emacs` to creat Emacs config file then insert the following to make your 
very preliminary hacks: 
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

## Install packages
To install a new package, first press `M-x` and type `package-refresh-contents` to fetch all packages and then use 
`M-x package-install` and enter the new package's name. To see list of the available packages use `M-x package-list-packages`. 
For example you can install Markdown-mode, htmlize and ESS packages with:
```
M-x package-install markdown-mode
M-x package-install htmlize
M-x package-install ess
```

To delete packages, use `M-x package-delete` and enter the package's name. Note that you may use `C-s`/`C-r` for searching and 
`C-g` to cancel any actions and `q` to close buffers in Emacs. 

## Customize faces
An easy way to change the appearance of Emacs is changing faces. `M-x list-faces-display` shows all of the faces that currently defined and you may modify them (use GUI Emacs to access them by clicking). To customize certain faces, use `M-x customize-face` and select the face that you wnat to change (press tab to see all options).

Also, you can customize faces from `.emacs` config file. For instance:
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

To change the theme, `M-x load-theme`, then press `tab` to show a list of available themes. To clear theme, `M-x disable-theme`. 

