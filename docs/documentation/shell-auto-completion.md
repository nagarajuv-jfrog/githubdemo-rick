---
title: Shell Auto Completion
deprecated: false
hidden: false
metadata:
  robots: index
---
<br />

If you're using JFrog CLI from a bash, zsh, or fish shell, you can install JFrog CLI's auto-completion scripts to improve your command-line experience. Auto-completion helps save time and reduces errors by suggesting potential command options and arguments as you type.

Auto-completion allows you to:

Increase Efficiency: Quickly fill in commands and arguments without typing them out fully.

Reduce Errors: Minimize typographical errors in commands and options.

Discover Commands: Easily explore options for specific commands with in-line suggestions.

What is JFrog CLI? : JFrog CLI is a command-line interface for interacting with JFrog Artifactory and other JFrog products. It simplifies various functions, such as uploading or downloading files, managing repositories, and more. For more information, refer to the JFrog CLI.

How to Enable Auto-Completion?: The method of enabling auto-completion varies based on the shell you are using (bash, zsh, or fish).

Install JFrog CLI with Homebrew: If you're installing JFrog CLI using Homebrew, the bash, zsh, or fish auto-complete scripts are automatically installed. However, you need to ensure that your
.bash_profile
or
.zshrc
files are correctly configured. Refer to the Homebrew Shell Completion documentation for specific instructions.

Using Oh My Zsh?
If you are using the Oh My Zsh framework, follow these steps to enable JFrog CLI auto-completion:

Open your zsh configuration file, located at
$HOME/.zshrc
, with any text editor."

your-text-editor $HOME/.zshrc

Locate the line starting with
plugins=
.

Add
jfrog
to the list of plugins. For example:

plugins=(git mvn npm sdk jfrog)

Save and close the file.

Finally, apply the changes by running:

source $HOME/.zshrc

Other Installation Methods
If you're not using Homebrew or Oh My Zsh, you can manually install the auto-completion scripts for your specific shell:

For Bash

To install auto-completion for bash, run the following command:

jf completion bash --install
⧉
Follow the on-screen instructions to complete the installation.

For Zsh

To install auto-completion for zsh, run the following command:

jf completion zsh --install
⧉
Again, follow the instructions provided during the installation process.

For Fish

To install auto-completion for fish, run the following command:

jf completion fish --install
⧉
Ensure you follow the relevant instructions to finalize the setup.

Verifying Installation
After installing the completion scripts, you can verify that auto-completion works by typing
jf
followed by pressing the
Tab
key. You should see a list of available commands and options.
