# Some configs for Mac terminal 

### Zsh (or Bash) config
Open (create if not exist) `.zshrc` (or `.bash_profile` if using bash) file in the home directory and add the following commands:

- `grep` default color option: `alias grep='grep --color=auto'`
- `ls` colored directories: `alias ls='ls -G'`
- `git` tab completion: `autoload -Uz compinit && compinit`
- Prompt format (Zsh only): `PROMPT="%F{green}%n@%m%f %F{blue}%1~%f $ "`

The following is a smiple `.zshrc` file:

```bash
# Simple prompt format
PROMPT="%F{green}%n@%m%f %F{blue}%1~%f $ "

# Autoload tab completions
autoload -Uz compinit && compinit

# My aliases
alias ls='ls -G'
alias ll='ls -lh'
alias grep='grep --color=auto'
alias emacs='emacs -nw'
alias nano='nano -z'
```

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

### Python 3
Select an option based on your requirements:

**Option 1 - Xcode:** To access Python 3 (an older version) and other command line tools, install Xcode Command Line Tools by running the following command in the terminal:

```bash
xcode-select --install
```

Only press `install` and ignore `get Xcode`. 

**Option 2 - Python:** To install a newer version of Python on a Mac without using a package manager like Homebrew, you can download and install it directly from the official Python website. Here’s how:

1. **Download the Python installer:**
   - Go to the [official Python website](https://www.python.org/).
   - Navigate to the "Downloads" section and select the latest stable version for macOS.

2. **Run the installer:**
   - Once the `.pkg` file has downloaded, open it to run the Python installer.
   - Follow the on-screen instructions to install Python.

3. **Verify the installation:**
   - Open a terminal and check the Python version by running:
     ```bash
     python3 --version
     ```
     or
     ```bash
     python3.x --version  # Replace x with the specific version number
     ```
   - This should display the newly installed Python version.

4. **Update your PATH (if necessary):**
   - Depending on your setup, you might need to add the new Python version to your PATH to make it the default. 
   - You can add the following line to your shell profile file (`.zshrc` or `.bash_profile`), replacing `/path/to/python3.x` with the actual path where Python was installed:
     ```bash
     export PATH="/path/to/python3.x:$PATH"
     ```
   - Reload your profile by running `source ~/.zshrc` (or the relevant profile file).

5. **Set up `python` as an alias for `python3` (optional):**
   - To simplify commands, you can create an alias for `python3` as `python` in your profile file:
     ```bash
     alias python=python3
     ```
   - Reload the profile with `source ~/.zshrc`.

**Option 3 - Miniconda:** You can also install Miniconda to access Python. Follow the instructions [here](https://docs.conda.io/projects/miniconda/en/latest/index.html#quick-command-line-install) to install and [here](https://docs.continuum.io/free/anaconda/install/uninstall/) to uninstall.

**Option 4 - Pyenv:** A newer Python version can be installed by [Pyenv](https://github.com/pyenv/pyenv). Pyenv can be installed by following [here](https://github.com/pyenv/pyenv#installation) and setting up the [environment setups](https://github.com/pyenv/pyenv#set-up-your-shell-environment-for-pyenv).    

After installation, use `Python3` to open Python and use [Venv](https://ashki23.github.io/python-env.html#venv) to create envs and install packages using pip.

### R
R can be installed from binary from [R mirror](https://mirror.las.iastate.edu/CRAN/). To [uninstall R](https://cran.r-project.org/doc/manuals/r-release/R-admin.html#Uninstalling-under-macOS), run the following:

```
sudo rm -rf /Library/Frameworks/R.framework
sudo rm -rf /Applications/R.app
sudo rm -rf /usr/local/bin/R
sudo rm -rf /usr/local/bin/Rscript
```

### Emacs
You can install Emacs [manually](https://github.com/ashki23/Linux-notes/blob/master/install-emacs-binary.md) or take the easier route by downloading it from [here](https://emacsformacosx.com). If you choose to download, create a symbolic link using the following command to access Emacs from the terminal:

```bash
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

### Pandoc
To install Pandoc on a Mac, you can download the latest release directly from the [Pandoc website](https://pandoc.org/installing.html). Here are the steps:
- Download the latest release for macOS (it should be a `.pkg` file).
- Open the downloaded `.pkg` file by double-clicking on it. This will launch the installer. The installer will place the `pandoc` executable in `/usr/local/bin` by default.

When a new version of Pandoc is released, you’ll need to repeat this process to update it. Just download the latest `.pkg` file and install it, which will overwrite the older version.
