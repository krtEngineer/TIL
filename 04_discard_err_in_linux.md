### Discard error messages in Linux

In Linux, managing output from commands is a crucial aspect of scripting and system administration. Sometimes, you may want to discard error messages to keep your output clean or to prevent them from interrupting your script's execution.

### Redirecting stderr to /dev/null

Command Syntax: command 2>/dev/null

```bash
kushagratiwari$ ls /nonexistent_directory
ls: /nonexistent_directory: No such file or directory
kushagratiwari$ ls /nonexistent_directory 2>/dev/null
kushagratiwari$
```

### What is /dev/null?

In Linux, **/dev/null** is a special file that acts as a data sink. It discards all data written to it, effectively **throwing it away.** This makes it useful for redirecting output that you want to ignore.

Happy scripting!
