---
title: Shell Auto Completion
excerpt: >-
  Generate shell completion scripts for JFrog CLI commands, including bash, zsh,
  and fish.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
## JFrog Completion

Generate shell completion scripts for JFrog CLI commands.

<br />

/*
commented text is
ignored by parser
*/

<br />

<br />

<Tabs>
  <Tab title="First Tab">
    Trust can be created between multiple services: you need to make sure that all participating instances in the circle of trust are equipped with the relevant public keys (root certificate). Note that a trust can be unidirectional or bidirectional. The service watches a directory of trusted public keys and reloads the keys when it needs to verify a token
  </Tab>

  <Tab title="Second Tab">
    | ID  | Name       | Status    | Score | Notes                     |
    | --- | ---------- | --------- | ----- | ------------------------- |
    | 101 | Alpha Wolf | Active    | 89    | Passed initial screening  |
    | 102 | Beta Hawk  | Inactive  | 72    | Needs follow-up review    |
    | 103 | Delta Fox  | Pending   | 94    | High potential candidate  |
    | 104 | Sigma Bear | Active    | 63    | Requires performance plan |
    | 105 | Omega Lynx | Suspended | 47    | Policy violation flagged  |
  </Tab>

  <Tab title="Third Tab">
    ```
    def calculate_metrics(values):
    total = sum(values)
    avg = total / len(values)
    return {
        "total": total,
        "average": round(avg, 2),
        "max": max(values),
        "min": min(values)
    }

    data = [12, 45, 3, 67, 23]
    result = calculate_metrics(data)

    print("Metrics:", result)

    ```
  </Tab>
</Tabs>

### Synopsis

The completion command generates shell completion scripts for bash, zsh, and fish. Shell completion enables interactive command-line completion of JFrog CLI commands, subcommands, and flags using the Tab key.

To load completions in your current shell session, follow the instructions provided for your shell after running the completion command.

### Usage

```
jfrog completion [shell] [flags]
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
jfrog completion bash
```

**Install bash completion automatically:**

```bash
jfrog completion bash --install
```

**Generate zsh completion script:**

```bash
jfrog completion zsh
```

**Install zsh completion automatically:**

```bash
jfrog completion zsh --install
```

**Generate fish completion script:**

```bash
jfrog completion fish
```

**Install fish completion automatically:**

```bash
jfrog completion fish --install
```

***

## Setup Instructions

### Prerequisites

JFrog Artifactory maintains download statistics for repositories so you can evaluate if artifacts are still being used and manage your cleanup policies. When you proxy a repository in another instance of JFrog Artifactory and cache an artifact downloaded from the other instance, the distant JFrog Artifactory is not aware if users on your end continue to use the artifact (by downloading it from your local cache), and may end up cleaning up the original artifact. A JFrog Artifactory Smart Remote Repository lets you notify the distant instance whenever a cached artifact is downloaded, so it can update an internal counter for remote downloads.

Shell completion requires your shell's completion system to be configured. Most package managers handle this automatically.

<Accordion title="My Accordion Title" icon="fa-info-circle">
  acxadcvdavasv  ad minim veniam, quis nostrud exercitation ullamco. Excepteur sint
  occaecat cupidatat non proident!
</Accordion>

<br />

<Cards columns={4}>
  <Card title="First Card" href="https://readme.com" icon="fa-home" target="_blank">
    Neque porro quisquam est qui dolorem ipsum quia
  </Card>

  <Card title="Second Card" icon="fa-user">
    *Lorem ipsum dolor sit amet, consectetur adipiscing elit*
  </Card>

  <Card title="Third Card" icon="fa-star">
    > Ut enim ad minim veniam, quis nostrud ullamco
  </Card>

  <Card title="Fourth Card" icon="fa-question">
    **Excepteur sint occaecat cupidatat non proident**
  </Card>
</Cards>

<Columns layout="auto">
  <Column>
    Neque porro quisquam est qui dolorem ipsum quia
  </Column>

  <Column>
    *Lorem ipsum dolor sit amet, consectetur adipiscing elit*
  </Column>

  <Column>
    > Ut enim ad minim veniam, quis nostrud ullamco
  </Column>
</Columns>

<br />

<br />

<Tabs>
  <Tab title="First Tab">
    Welcome to the content that you can only see inside the first Tab.
  </Tab>

  <Tab title="Second Tab">
    Here's content that's only inside the second Tab.
  </Tab>

  <Tab title="Third Tab">
    Here's content that's only inside the third Tab.
  </Tab>
</Tabs>

<br />

> faDCAdcaDXA

<br />

<Callout icon="📘" theme="info">
  ScaC ac
</Callout>

/

<br />

### Bash

**macOS (using Homebrew):**

```bash
brew install bash-completion@2
```

```markdown
brew install bash-completion@2 sbsdbs
```

<br />

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
jfrog completion bash --install
```

Alternatively, generate the script manually:

```bash
jfrog completion bash > /usr/local/etc/bash_completion.d/jfrog
```

Reload your shell:

```bash
source ~/.bash_profile  # macOS
source ~/.bashrc        # Linux
```

### Zsh

**Standard zsh:**

Install completion:

```bash
jfrog completion zsh --install
```

Follow the on-screen instructions to add the completion script location to your `fpath`.

Alternatively, generate the script manually:

```bash
# Create completion directory if needed
mkdir -p ~/.zsh/completion

# Generate completion script
jfrog completion zsh > ~/.zsh/completion/_jfrog
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

### Fish

**Install completion:**

```bash
jfrog completion fish --install
```

Alternatively, generate the script manually:

```bash
jfrog completion fish > ~/.config/fish/completions/jfrog.fish
```

Completions will be available in new shell sessions.

***

## Verification

After installation, test the completion:

1. Open a new terminal session
2. Type `jfrog ` and press `Tab`
3. You should see available commands
4. Type `jfrog config ` and press `Tab` to see subcommands

Example output:

```
$ jfrog <Tab>
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
sudo jfrog completion bash --install
```

**Oh My Zsh plugin not found:**

Ensure you have the latest version of Oh My Zsh and that the JFrog CLI is installed via Homebrew or the plugin is available in your Oh My Zsh installation.

***

## See Also

* [jfrog config](./config.md) - Configure JFrog CLI settings
* [jfrog --help](./help.md) - Get help for any command
* [Environment Variables](./environment-variables.md) - Configure CLI behavior with environment variables

***
