# Install Emacs on Mac Terminal

To install Emacs for use in the terminal only on a Mac without a package manager, you can download the Emacs source code, build it manually, and configure it to be run from the terminal. This installation will not include the graphical (GUI) version of Emacs, only the terminal (CLI) version.

Here's how to do it:

### Step 1: Download the Emacs Source Code

1. Visit the official [GNU Emacs website](https://www.gnu.org/software/emacs/) or the [GNU FTP site for Emacs](https://ftp.gnu.org/gnu/emacs/) to get the latest release.
2. Download the `.tar.gz` file for the latest Emacs release (e.g., `emacs-28.1.tar.gz`).

Alternatively, you can download the file directly using `curl` from the Terminal:

```bash
curl -O https://ftp.gnu.org/gnu/emacs/emacs-28.1.tar.gz
```

### Step 2: Extract the Tarball

After downloading, extract the tarball:

```bash
tar -xzvf emacs-28.1.tar.gz
```

Navigate into the extracted directory:

```bash
cd emacs-28.1
```

### Step 3: Configure the Build for Terminal-Only

To build Emacs for terminal use only, configure it to disable the GUI options:

```bash
./configure --without-x --without-ns --without-cocoa
```

Explanation of the options:
- `--without-x`: Disables X11 support.
- `--without-ns`: Disables the macOS "NextStep" GUI support.
- `--without-cocoa`: Disables the Cocoa framework, which is used for GUI on macOS.

### Step 4: Build Emacs

Compile Emacs with the `make` command:

```bash
make
```

This process may take a few minutes.

### Step 5: Install Emacs

After building, you can install it using:

```bash
sudo make install
```

This installs Emacs in `/usr/local/bin` by default, which should be in your PATH, allowing you to run it from the terminal by simply typing `emacs`.

### Step 6: Verify the Installation

To verify that Emacs is installed correctly, type:

```bash
emacs --version
```

You should see the version number of Emacs displayed, confirming that it is installed.

### Running Emacs in the Terminal

Now, you can open Emacs in the terminal by simply typing:

```bash
emacs
```

This will launch Emacs in terminal mode without any GUI features.

### Optional Cleanup

You can delete the downloaded files and the extracted directory to save space if you no longer need them:

```bash
cd ..
rm -rf emacs-28.1 emacs-28.1.tar.gz
```

That's it! You now have a terminal-only installation of Emacs on macOS without using a package manager.

### Important Note
Since you’re installing manually from source, there’s no automatic update process. You’ll need to repeat this procedure each time a new version of Emacs is released if you want to stay up-to-date. This will overwrite the previous version installed in `/usr/local/bin`.
