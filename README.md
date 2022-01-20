# terraform-on-m1-mac
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](./LICENSE)

Apple has release a [micro-processor chip called M1](https://www.apple.com/newsroom/2020/06/apple-announces-mac-transition-to-apple-silicon/). Which is highly compartible to thier computers, with much better efficiency compared to intel chips. If you have embraced this change, you might find a few difficulty leveraging the new product, due to compatibility issues. Here are the patterns for making the move from Intel to M1.

## Install Homebrew
Homebrew is an open-source package mangaer for macOS, which offers an easy way to install softwares via comand line. It also helps you use commands to download and install Python, Ruby, cask, Nmap, MongDB and other Unix CLI utilities like terraform etc.

### Requirements to install Homebrew on Mac M1

- Apple Silion M1 CPU
- macOS Mojave (10.14) or later
Command Line tools for Xcode (Some formulae and softwares require Xcode installed)
- Compatible shell for installation (bash or zsh)

### How to install Homebrew on Mac M1
1. From your Terminal enter this command `xcode-select --install`
2. Follow the instructions from the popup to complete the installation
3. Enter the following command in the Terminal. `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
4. verify your installation by typiing `brew -v`

### Installing Rosetta 2 on Mac M1
Rosetta 2 is needed for easy transitioning from Macs running on Intel processors to Apple silicon processors. It allows most intel apps to run on Apple Silicon without issues, enabling software vendors to provide universal updates and builds for both Intel and Aplle Silicon.
1. Run the following command to install rosetta 2. `/usr/sbin/softwareupdate --install-rosetta --agree-to-license`
2. If you want to confirm the installation process, copy the shell script in this repo.
3. The script will either enforce the installation, or confirm the installation. Give the shell script execution priviledges `chmod +x install_rosetta_on_apple_silicon.sh`
4. Run the shell script in the terminal `./install_rosetta_on_app_silicon.sh`
5. the output should be `"Rosetta is already installed and running. Nothing to do."`
6. You may need to restart your computer to start seeing the uses of rosseta 2. Enjoy!! :)

### Installing Terraform on Mac M1

Some people have issues installing Terraform on Mac M1. If you have installed Rosetta 2, and restarted your computer, you should not have any issues. But, should you still have issues, run the following command.
1. `brew install --build-from-source terraform`
2. You should be able to run `terraform init` on any repository.