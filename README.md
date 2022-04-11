# terraform-on-m1-mac
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](./LICENSE)

Apple has release a [micro-processor chip called M1](https://www.apple.com/newsroom/2020/06/apple-announces-mac-transition-to-apple-silicon/). Which is highly compartible to thier computers,, with much better efficiency compared to intel chips. If you have embraced this change, you might find a few difficulty leveraging the new product, due to compatibility issues. Here are the patterns for making the move from Intel to M1.

## Install Homebrew
Homebrew is an open-source package mangaer for macOS, which offers an easy way to install softwares via comand line. It also helps you use commands to download and install Python, Ruby, cask, Nmap, MongDB and other Unix CLI utilities like terraform etc.

### Requirements to install Homebrew on Mac M1

- Apple Silion M1 CPU
- macOS Mojave (10.14) or later
Command Line tools for Xcode (Some formulae and softwares require Xcode installed)
- Compatible shell for installation (bash or zsh)

### How to install Homebrew on Mac M1
1. From your Terminal enter this command `$ xcode-select --install`
2. Follow the instructions from the popup to complete the installation
3. Enter the following command in the Terminal: 
```shell
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install)"
```
4. verify your installation by typing `$ brew -v`

### Installing Rosetta 2 on Mac M1
Rosetta 2 is needed for easy transitioning from Macs running on Intel processors to Apple silicon processors. It allows most intel apps to run on Apple Silicon without issues, enabling software vendors to provide universal updates and builds for both Intel and Aplle Silicon.
1. Run the following command to install rosetta 2. 
```shell
$ /usr/sbin/softwareupdate --install-rosetta --agree-to-license
```
2. If you want to confirm the installation process, copy the shell script in this repo.
3. The script will either enforce the installation, or confirm the installation. Give the shell script execution priviledges `chmod +x install_rosetta_on_apple_silicon.sh`
4. Run the shell script in the terminal `./install_rosetta_on_app_silicon.sh`
5. the output should be `"Rosetta is already installed and running. Nothing to do."`
6. You may need to restart your computer to start seeing the uses of rosseta 2. Enjoy!! :)

7. Some M1 chips have issues installing some apps on M1 chips after installing rosetta 2, if that was your case, please consider the following steps from 8. Note: since the Rosetta emmulated intel processor independently uses /usr/local/ for intel based homebrews, which differs from the /opt/homebrew for M1 chip (ARM64), you may need a seprate homebrew for the rosetta homebrew emulator. You could Either leverage a different terminal (e.g. iterm) for Rosetta related brews, or combining both in same terminal using aliases, this helps in case you forget which terminal is for M1.

8. Combining both in one terminal using the `/usr/local`:
```shell
$ arch -x86_64 zsh
$ cd /usr/local && mkdir homebrew
$ curl -L https://github.com/Homebrew/brew/tarball/master | tar xz --strip 1 -C homebrew
```
>After Homebrew is up and running, you can levrage the architecture flags in your installations as Rosetta gives us the ability to prefix commands. 
9.  Installing the packages using intel, you can use the following:
    ```bash
    % arch -x86_64 /usr/local/homebrew/bin/brew install <package name>
    ```
10. Installing the packages using intel, you can use the following:
    ```bash
    % /opt/homebrew/bin/brew install <package name>
    ```
11. To simplify the above, I would rather make use of aliases rather that remembering the above line.
    ```bash
     # ~/.zshrc
    alias ibrew='arch -x86_64 /opt/homebrew/bin/brew'
    alias mbrew='arch -arm64e /usr/local/bin/brew'
    ```
    Thus you use `mbrew install <package name>` or `ibrew install <package name>`
12. You can further add the path with preference to M1 version over intel with the following configurations 
    ```bash
    # ~/.zshrc
    typeset -U path;
    path+=(/usr/local/bin);
    path+=(/opt/homebrew/bin);
    ```
13. If you have Python (<3.9), you may encounter some issues, to resolve them run the following:
    ```bash
    % arch -x86_64 pip install --upgrade pip setuptools
    ```

14. Should you have problems opening Rosetta terminal(shell) run the following:
    ```shell
    % arch -x86_64 zsh
    ```

### Installing Terraform on Mac M1

Some people have issues installing Terraform on Mac M1. If you have installed Rosetta 2, and restarted your computer, you should not have any issues. But, should you still have issues, run the following command.
```shell
% mbrew install --build-from-source terraform
```
