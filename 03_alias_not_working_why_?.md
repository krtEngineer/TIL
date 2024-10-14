Date: 14/10/2024

### Alias might not work in bash scripts. Why?

Aliases in Bash are a convenient way to create shortcuts for long or complex commands. They work seamlessly in interactive shells, making it easy to streamline your workflow. However, when you try to use aliases in Bash scripts, you might find that they don't work as expected. Let's explore why this happens and how you can enable alias expansion within scripts.

![Alias_Error](https://github.com/krtEngineer/TIL/blob/main/assets/03_image_1.png?raw=true)

### Why Aliases Don't Work in Scripts

By default, aliases are not expanded in non-interactive shells, such as those used when running a script. This behavior is intentional and is designed to maintain script portability and predictability. Here’s why:

**Script Portability**: Scripts should behave consistently across different environments. If aliases were expanded by default, scripts might behave unpredictably if they relied on user-defined aliases that vary from system to system.

**Performance**: Expanding aliases in scripts could introduce unnecessary overhead, affecting performance, especially in complex scripts.

**Security**: Aliases can change the behavior of commands in unexpected ways, potentially introducing security risks if scripts execute unintended commands.

### How to Enable Alias Expansion in Scripts?

If you really need to use aliases in your scripts, you can enable their expansion by explicitly allowing it. Here’s how you can do it:

**Use the shopt Command**
You can enable alias expansion by using the shopt command with the expand_aliases option at the beginning of your script.

```bash
#!/bin/bash

# Enable alias expansion
shopt -s expand_aliases

# Define your aliases
alias greeting='echo Namaste'

# Use the alias
greeting
```

**Source the Script**
Another method is to source the script in an interactive shell. This way, the script runs in the current shell environment where aliases are already available.

```bash
source my_script.sh
```

**Alternative: Use Functions**
Instead of relying on aliases, consider using functions, which are more robust and script-friendly.

```bash
#!/bin/bash

# Define a function
greeting() {
    echo Namaste
}

# Use the function
greeting
```

Functions provide similar benefits to aliases but are more flexible and powerful, making them a better choice for scripts.
