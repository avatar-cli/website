+++
title = "Weekly Report #01"
description = "Avatar-CLI's weekly development report"
date = 2020-09-10
+++

*Note: This post was first published as a
[Slack note](https://slack-files.com/TBUA4NSQZ-F01AG72AYDQ-2b5a50a74c).*

This is the first weekly report I write for this project, here or anywhere else,
and I'm happy to begin this tradition.

## New Release (v0.18.0)

- Improved support for JetBrains IDEs (specifically PHPStorm): Now avatar
  install generates wrapper shell scripts that can be used by IDEs to use
  dockerized interpreters (like PHP or Python) without having to create a
  subshell with avatar shell or modify the environment with
  `source <(avatar export-env)`.
- Fixed OCI (Docker) images generation, that were broken after a regression.
- Improved documentation, clarified minor details.

## Work in Progress (in `dev` branch, not released)

- More documentation improvements:
    - Added new informative badges to the README.md file.
    - Added a "Community" section, linking the Discord space & the Twitter
      official account.
    - New minor clarifications on the "How to install" section.

## Community

- Started collaboration with Project Unicorn :smile: .
- Created [new Discord workspace](https://discord.gg/8ek44UM)!
- We have a first external contributor (work still in progress on
  [error handling](https://gitlab.com/etra0/avatar-cli/-/commits/feature/error-handling),
  but quite promising 🙂)

## Near Future Plans

- Website preparation ( [avatar-cli.dev](https://www.avatar-cli.dev) ).
- There are some ongoing discussions with a user on how to use docker-compose
  configurations to make possible orchestrating complex integration tests with
  Avatar-CLI. This same functionality was implemented in the old privative
  predecessor of Avatar-CLI (that was written using Bash), but it cannot be
  directly ported as it is, since it requires more generality & guarantees of
  forward-compatibility.
