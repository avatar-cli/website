+++
title = "Troubleshooting"
weight = 6
+++

## Interactive Git Hooks using tools managed by Avatar-CLI

Git hooks are non-interactive by default, if you want to transform them into
interactive programs, the program must connect its standard input to a
pseud-tty device (usually `/dev/tty`) by itself.

If such git hooks use tools managed by Avatar, you must ensure that the TTY
attachment is performed before any managed container is spawned, because once
the container has been already connected and started, there's no sensible
way to attach a terminal to it for Avatar-CLI.

One example for the mentioned problem is the combination of tools such as
NodeJS, Husky and Commitizen. Husky will start a shell script for each git hook,
and pass the control of execution to `npm` after some checks.

In the specific case of Avatar-CLI, we solved this problem by creating a patch
for Husky ([PR #747](https://github.com/typicode/husky/pull/747)), and [forking
the project](https://www.npmjs.com/package/@coderspirit/husky-fork) while the
Husky project mantainers decide whether to accept this PR or not.

## Customized `$PATH` environment variable

In case you have a customized `$PATH` environment variable via configuration
scripts like `~/.bashrc`, you should wrap that redefinition with a conditional
statement to avoid breaking how Avatar-CLI works.

For example, something like this:
```bash
export PATH="/custom/extra/bin/path:${PATH}";
```

Should be converted into this:
```bash
if [ -z "${AVATAR_CLI_SESSION_TOKEN}" ]; then
  export PATH="/custom/extra/bin/path:${PATH}";
fi
```

Don't worry, the paths you declared are still available, but Avatar-CLI must be
sure that its own managed paths are the first ones to be evaluated.
