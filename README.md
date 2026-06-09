# Claude Auto Accept

A simple terminal wrapper tool that automatically bypasses and accepts permission prompts for the Claude Code CLI, particularly useful for organizations that have disabled the `--dangerously-skip-permissions` flag.

## How it works

This tool uses macOS's built-in `expect` utility to spawn the `claude` CLI and act as a transparent proxy. It continuously listens to the output stream, and the millisecond it detects the text asking for permission (e.g. `Do you want to proceed?`), it automatically types `y` and presses `Enter`. 

It completely ignores standard conversational outputs and only triggers on the exact prompt you define.

## Setup & Installation

1. Make sure the script is executable:
   ```bash
   chmod +x claude-auto.exp
   ```

2. Test it locally by running:
   ```bash
   ./claude-auto.exp
   ```

3. **(Recommended)** Create an alias in your shell profile (e.g., `~/.zshrc` or `~/.bashrc`) so you can run it globally:
   ```bash
   echo 'alias claude-auto="/path/to/claude-auto-accept/claude-auto.exp"' >> ~/.zshrc
   source ~/.zshrc
   ```

## Usage

Instead of typing `claude` in your terminal, type `claude-auto`.

```bash
claude-auto "your prompt here"
```

## Customization

If the Claude CLI updates its prompt text, you can easily modify the script by editing the `claude-auto.exp` file and changing the `-re` string matcher:

```tcl
    # Match specifically "Do you want to proceed?", ignoring case
    -re "(?i)Do you want to proceed\\\?" {
        send "y\r"
    }
```
