# Some configs for mac terminal 

### Zsh (or Bash) config
Open (create if not exist) `.zshrc` (or `.bash_profile` if using bash) file in home directory and add the following commands:

- `grep` default color option: `alias grep='grep --color=auto'`
- `ls` colored directories: `alias ls='ls -G'`
- `git` tab completion: `autoload -Uz compinit && compinit`

**Note:** After adding above commands, use `source .zshrc` to apply changes.

### Use Option as Meta key
To active this option, open `Terminal > Prefences` and select `Keyboard` tab and check `Use Option as Meta key`.

### Exit shell and close the window
To be able to close terminal window by `ctrl + d`, open `Terminal > Prefences` and select `Shell` tab and change `When the shell exits` to `Close the window`.

### Increase the cursor speed
Go to the `System Preferences > Keyboard`, make `Key Repeat` faster and `Delay Until Repeat` shorter.

### SSH
To be able use ssh without asking for the passphrase, we need to add the passphrase to a ssh-agent. Note in here we are adding `id_rsa` key. First, let's start the ssh-agent in the background:

```bash
eval `ssh-agent -s`
```

After that open (or create) `~/.ssh/config` file and add:

```bash
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

Now run the following to add your SSH private key to the ssh-agent and store your passphrase in the keychain:

```bash
ssh-add -K ~/.ssh/id_rsa
```

You may find more details in [here](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

### Python3
To have python3 and many more command line tools, install `xcode-select`. Use the following command in the terminal for installation:

```bash
xcode-select --install
```

**Note:** Only press `install` and ignore `get Xcode`.

### R
R can be installed from binary from [R mirror](https://mirror.las.iastate.edu/CRAN/). To [uninstall R](https://cran.r-project.org/doc/manuals/r-release/R-admin.html#Uninstalling-under-macOS), run the following:

```
sudo rm -rf /Library/Frameworks/R.framework
sudo rm -rf /Applications/R.app
sudo rm -rf /usr/local/bin/R
sudo rm -rf /usr/local/bin/Rscript
```

### Emacs
Download Emacs from [here](https://emacsformacosx.com) and create a symbolic link from Emacs to `/usr/local/bin` by:

```
sudo ln -s /Applications/Emacs.app/Contents/MacOS/Emacs /usr/local/bin/emacs
```

Another option (better!) is crreating a virtual Conda env for Emacs.

To set `emacs -nw` as default add the following line to the `.zshrc` (or `.bash_profile`):

```bash
alias emacs='emacs -nw'
```

As a basic Emacs config, create `.emacs` file in the home directory and add the following:
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
