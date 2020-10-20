+++
title = "Getting Started"
weight = 0
+++

## Introduction

Avatar-CLI is a command line tool that allows you to run thousands of cli
programs for your dev projects without having to install them in your system.
You can see it as a sort of Python's "virtual env" for containerized software.

It can ease the development forkflow in many ways:
  - Making possible version-pinning for any kind of tool used in any kind of
    project. No need for complex setups or ultra-specific tools like
    [`nvm`](https://github.com/nvm-sh/nvm),
    [`nodeenv`](https://ekalinin.github.io/nodeenv/),
    [`pyenv`](https://github.com/pyenv/pyenv),
    [`rbenv`](https://github.com/rbenv/rbenv),
    [`goenv`](https://github.com/syndbg/goenv),
    [`asdf-vm`](https://asdf-vm.com), ... I guess you already have seen the
    pattern.
  - Making possible for new contributors to be productive from the very first
    minute, reducing the bootstrap/setup time to almost zero. Only `git` and
    `docker` are required.

## Why?

Why Avatar-CLI exists and what problems does it try to solve?

- Avatar-CLI was created to shorten setup time of development environments to
  near-zero.
- Avatar-CLI lets each project define its development environment as code and
  share it through source control as a configuration file. See the
  [Avatarfile documentation](/documentation/avatarfile/).

Problems solved by Avatar-CLI and surrounding practices:

- *Works on my machine* - With Avatar-CLI, each developer (and/or CI agent) gets
  a consistent and reproducible environment built with a combination of docker
  images.
- Avatar-CLI helps to fight configuration drift. Tools and configurations in the
  CI/CD environments and developers' environments tend to accumulate differences
  and mismatches over time. Avatar-CLI allows using exactly the same tools,
  having a single source of truth for their configuration.

## Similar projects

### [Dojo](https://github.com/kudulab/dojo)

Developed in Go. It requires highly customized image definitions.

### [Lando](https://lando.dev/)

Developed in Javascript. Perhaps the most advanced project in this space, with
a big community and dozens of recipes to prepare environments. It's an
abstraction layer on top of Docker and Docker-Compose, and it allows to override
its default behaviour with lower level configurations.

### [Toolbox](https://github.com/containers/toolbox)

Developed in Go. It uses a single mutable container where all the development
dependencies are installed.
