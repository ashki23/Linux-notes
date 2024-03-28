# Some configs for Mac terminal 

### Zsh (or Bash) config
Open (create if not exist) `.zshrc` (or `.bash_profile` if using bash) file in the home directory and add the following commands:

- `grep` default color option: `alias grep='grep --color=auto'`
- `ls` colored directories: `alias ls='ls -G'`
- `git` tab completion: `autoload -Uz compinit && compinit`

**Note:** After adding the above commands, use `source .zshrc` to apply changes.

### Use Option as Meta key
To activate this option, open `Terminal > Prefences` and select `Keyboard` tab, and check `Use Option as Meta key`.

### Exit the shell and close the window
To be able to close the terminal window by `ctrl + d`, open `Terminal > Prefences` and select `Shell` tab, and change `When the shell exits` to `Close the window`.

### Increase the cursor speed
Go to the `System Preferences > Keyboard`, and make `Key Repeat` faster and `Delay Until Repeat` shorter.

### SSH
To be able to use ssh without asking for the passphrase, open (or create) `~/.ssh/config` file and add:

```bash
Host *
  UseKeychain yes
  AddKeysToAgent yes
  ServerAliveInterval 60
  IdentityFile ~/.ssh/id_rsa
```

Now run the following to start ssh-agent and adding your SSH private key to the ssh-agent and store your passphrase in the keychain:

```bash
eval $(ssh-agent -s)
ssh-add --apple-use-keychain ~/.ssh/id_rsa
```

You may find more details in [here](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent). The following are two more config examples for GitHub and a GCP compute instance:
```bash
Host git
  HostName github.com
  User git
  UseKeychain yes
  AddKeysToAgent yes
  ServerAliveInterval 60
  IdentityFile ~/.ssh/id_rsa

Host gcp
  HostName <server.public.ip>
  UseKeychain yes
  AddKeysToAgent yes
  ServerAliveInterval 60
  IdentityFile ~/.ssh/id_rsa_gcp
```

We added `ServerAliveInterval` option to keep the ssh connection alive, but if you still have some ssh timeout issues, you may modify the following options in `/etc/ssh/sshd_config`:

```bash
ClientAliveInterval 60
ClientAliveCountMax 3
```

### Python3
To have python3 and many more command line tools, install `xcode-select`. Use the following command in the terminal for installation:

```bash
xcode-select --install
```

**Note:** Only press `install` and ignore `get Xcode`. After installation, use `Python3` to open Python and use [Venv](https://ashki23.github.io/python-env.html#venv) to create envs and install packages using pip.

A newer Python version can be installed by [Pyenv](https://github.com/pyenv/pyenv). Pyenv can be installed by following [here](https://github.com/pyenv/pyenv#installation) and setting up the [environment setups](https://github.com/pyenv/pyenv#set-up-your-shell-environment-for-pyenv).    

### Miniconda
Follow the instructions [here](https://docs.conda.io/projects/miniconda/en/latest/index.html#quick-command-line-install) to install and [here](https://docs.continuum.io/free/anaconda/install/uninstall/) to uninstall.

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
