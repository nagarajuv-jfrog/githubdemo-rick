---
title: Shell Auto Completion
deprecated: false
hidden: false
metadata:
  robots: index
---
<br />

# Shell Auto-Completion

## Overview

JFrog CLI supports shell auto-completion for bash, zsh, and fish shells. Auto-completion helps save time and reduces errors by suggesting potential command options and arguments as you type.

### Benefits

* **Increase Efficiency**: Quickly fill in commands and arguments without typing them out fully
* **Reduce Errors**: Minimize typographical errors in commands and options
* **Discover Commands**: Easily explore options for specific commands with in-line suggestions

## Installation

The method of enabling auto-completion varies based on the shell you are using.

### Installation via Homebrew

If you're installing JFrog CLI using Homebrew, the bash, zsh, or fish auto-complete scripts are automatically installed. However, you need to ensure that your `.bash_profile` or `.zshrc` files are correctly configured.

Refer to the [Homebrew Shell Completion documentation](https://docs.brew.sh/Shell-Completion) for specific instructions.

### Oh My Zsh Framework

If you are using the Oh My Zsh framework, follow these steps to enable JFrog CLI auto-completion:

1. Open your zsh configuration file, located at `$HOME/.zshrc`, with any text editor

2. Locate the line starting with `plugins=`

3. Add `jfrog` to the list of plugins. For example:

   ```bash
   plugins=(git mvn npm sdk jfrog)
   ```

4. Save and close the file

5. Restart your terminal or run `source ~/.zshrc`

### Manual Installation

If you're not using Homebrew or Oh My Zsh, you can manually install the auto-completion scripts for your specific shell.

#### bash

Run the following command to install bash completion:

```bash
jf completion bash --install
```

Follow the on-screen instructions to complete the installation.

#### zsh

Run the following command to install zsh completion:

```bash
jf completion zsh --install
```

Follow the on-screen instructions to complete the installation.

#### fish

Run the following command to install fish completion:

```bash
jf completion fish --install
```

Again, follow the instructions provided during the installation process.

## Verification

After installation, restart your terminal or source your shell configuration file to activate auto-completion. You can then test it by typing `jf` or `jfrog` followed by a space and pressing the Tab key to see available commands and options.

## Related Topics

* [JFrog CLI Installation](https://jfrog.com/help/r/jfrog-applications-and-cli-documentation/install)
* [JFrog CLI Environment Variables](https://jfrog.com/help/r/jfrog-applications-and-cli-documentation/jfrog-cli-environment-variables)
* [JFrog CLI Configuration](https://jfrog.com/help/r/jfrog-applications-and-cli-documentation/configurations)
