+++
title = "Commands"
weight = 3
+++

The commands are presented here in alphabetic order, but the most important ones
are [`init`](#init), [`shell](#shell), and [`run](#run).

## `export-env`

The command `avatar export-env`, if executed inside an Avatar-CLI project
directory, will output a list of shell export statements that define an
"environment".

It can be used in scripts to activate the tools managed by Avatar-CLI.

If you are using Bash scripts, you could "activate" the environment this way:
```bash
#!/bin/bash

source <(avatar export-env)
```

If you want full compatibility with POSIX shells, then you have to first create
a temporary file and then source it:
```bash
#!/bin/sh

avatar export-env > /your/temporary/file
. /your/temporary/file # Notice how we use '.' and not 'source'
```


## `help`

As you might expect, typing `avatar help` in the command line will show you some
help information:
```
avatar 0.18.1

USAGE:
    avatar <SUBCOMMAND>

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

SUBCOMMANDS:
    export-env    Prints shell variable exports to create a new Avatar-CLI session. Useful for scripts.
    help          Prints this message or the help of the given subcommand(s)
    init          It generates a new Avatar-CLI project configuration
    install       It 'installs' all the project stated dependencies
    run           Executes a wrapped project tool without having to enter into a subshell
    shell         Starts a new subshell exposing the wrapped project tools
```

You can also type `avatar help [subcommand]` to get more detailed information,
as an example, for `avatar help run` you would get:
```
avatar-run 
Executes a wrapped project tool without having to enter into a subshell

USAGE:
    avatar run <program_name> [program_args]...

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

ARGS:
    <program_name>       
    <program_args>...
```

## `init`

In case you are in a directory that has not been already initialized as an
Avatar-CLI project, by typing `avatar init` the project will be initialized.

The initialization consists on creating a new directory `.avatar-cli` and
placing inside a new [YAML](https://en.wikipedia.org/wiki/YAML) file called
[`Avatarfile`](/documentation/avatarfile). That's the file that we'll modify to
tweak our project.

## `install`

The command `avatar install` will update the "lock files" and ensure that all
the required OCI/Docker images are available.

In general terms, you won't have to use this command almost ever, as it's
implicitly triggered by the subcommands [`run`](#run) and [`shell`](#shell) if needed.

## `run`

Assuming that you have an already initialized project where you defined the
the software you want to run in your [`Avatarfile`](/documentation/avatarfile),
you could execute the desired program with the following command:
```bash
avatar run program_name
```

In case you want to pass parameters to the containerized application, you can do
it like this (notice the `--` between the program name and its parameters):
```bash
avatar run program_name -- param_1 param_2 ... param_n
```

As you can see, running the containerized applications like this can feel a
little bit cumbersome. The commands are slightly longer and complicated than
when we are running non-containerized applications... and that's why we have
the subcommand [`shell`](#shell) to overcome this issue.

## `shell`

When you type `avatar shell`, a new subshell will be created, where certain
environment variables will be available, and the containerized cli tools that
you configured in the [`Avatarfile`](/documentation/avatarfile) will be
available to you as if they were installed in your system.

For example, assuming that we don't have NodeJS installed in our system but
we configured it in our project, then it will be available to us:

```
» node
node: command not found

# With this command, we go into a new subshell...
» avatar shell

# And now `node` is available to us :D
» node --version
v14.14.0

» echo "console.log('hello')" | node
hello
```
