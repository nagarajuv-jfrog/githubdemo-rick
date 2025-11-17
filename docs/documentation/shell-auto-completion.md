---
title: Shell Auto Completion
deprecated: false
hidden: false
metadata:
  robots: index
---
<br />

## jf completion

Generate shell completion scripts for JFrog CLI commands.

### Synopsis

The completion command generates shell completion scripts for bash, zsh, and fish. Shell completion enables interactive command-line completion of JFrog CLI commands, subcommands, and flags using the Tab key.

To load completions in your current shell session, follow the instructions provided for your shell after running the completion command.

### Usage

```
jf completion [shell] [flags]
```

### Available Shells

* `bash`
* `zsh`
* `fish`

### Flags

```
--install    Install the completion script automatically
```

### Examples

**Generate bash completion script:**

```bash
jf completion bash
```

**Install bash completion automatically:**

```bash
jf completion bash --install
```

**Generate zsh completion script:**

```bash
jf completion zsh
```

**Install zsh completion automatically:**

```bash
jf completion zsh --install
```

**Generate fish completion script:**

```bash
jf completion fish
```

**Install fish completion automatically:**

```bash
jf completion fish --install
```

***

## Setup Instructions

### Prerequisites

Shell completion requires your shell's completion system to be configured. Most package managers handle this automatically.

### bash

**macOS (using Homebrew):**

```bash
brew install bash-completion@2
```

Add the following to your `~/.bash_profile`:

```bash
export BASH_COMPLETION_COMPAT_DIR="/usr/local/etc/bash_completion.d"
[[ -r "/usr/local/etc/profile.d/bash_completion.sh" ]] && . "/usr/local/etc/profile.d/bash_completion.sh"
```

**Linux:**

Most Linux distributions have bash-completion pre-installed. If not:

```bash
# Debian/Ubuntu
sudo apt-get install bash-completion

# RHEL/CentOS/Fedora
sudo yum install bash-completion
```

**Install JFrog CLI completion:**

```bash
jf completion bash --install
```

Alternatively, generate the script manually:

```bash
jf completion bash > /usr/local/etc/bash_completion.d/jf
```

Reload your shell:

```bash
source ~/.bash_profile  # macOS
source ~/.bashrc        # Linux
```

### zsh

**Standard zsh:**

Install completion:

```bash
jf completion zsh --install
```

Follow the on-screen instructions to add the completion script location to your `fpath`.

Alternatively, generate the script manually:

```bash
# Create completion directory if needed
mkdir -p ~/.zsh/completion

# Generate completion script
jf completion zsh > ~/.zsh/completion/_jf
```

Add to your `~/.zshrc`:

```bash
fpath=(~/.zsh/completion $fpath)
autoload -Uz compinit && compinit
```

Reload your shell:

```bash
source ~/.zshrc
```

**Oh My Zsh:**

If using Oh My Zsh, add `jfrog` to the plugins array in `~/.zshrc`:

```bash
plugins=(
  git
  docker
  kubectl
  jfrog
)
```

Reload your shell:

```bash
source ~/.zshrc
```

**Homebrew (automatic):**

When installing via Homebrew, completions are installed automatically:

```bash
brew install jfrog-cli
```

Ensure Homebrew completions are enabled in `~/.zshrc`:

```bash
if type brew &>/dev/null; then
  FPATH="$(brew --prefix)/share/zsh/site-functions:${FPATH}"
  autoload -Uz compinit && compinit
fi
```

### fish

**Install completion:**

```bash
jf completion fish --install
```

Alternatively, generate the script manually:

```bash
jf completion fish > ~/.config/fish/completions/jf.fish
```

Completions will be available in new shell sessions.

***

## Verification

After installation, test the completion:

1. Open a new terminal session
2. Type `jf ` and press `Tab`
3. You should see available commands
4. Type `jf config ` and press `Tab` to see subcommands

Example output:

```
$ jf <Tab>
add          completion   pip          use
build        config       rt           version
c            docker       scan         ...
```

***

## Troubleshooting

**Completions not working:**

1. Ensure the completion script is in the correct location
2. Verify your shell configuration file loads the completion system
3. Restart your terminal or source your configuration file
4. Check that the JFrog CLI binary is in your `$PATH`

**Permission errors during installation:**

If you encounter permission errors, you may need to run the command with `sudo` or adjust file permissions:

```bash
sudo jf completion bash --install
```

**Oh My Zsh plugin not found:**

Ensure you have the latest version of Oh My Zsh and that the JFrog CLI is installed via Homebrew or the plugin is available in your Oh My Zsh installation.

***

## See Also

* [jf config](./config.md) - Configure JFrog CLI settings
* [jf --help](./help.md) - Get help for any command
* [Environment Variables](./environment-variables.md) - Configure CLI behavior with environment variables

***

<br />
