+++
title = "Avatar-CLI"
in_search_index = false
+++

## Why?

Why Avatar-CLI exists and what problems it tries to solve?

- Avatar-CLI was created to shorten setup time of development environments to
  near-zero.
- Avatar-CLI lets each project define its development environment as code and
  share it through source control as a configuration file. See the
  [Avatarfile example](https://gitlab.com/avatar-cli/avatar-cli#avatarfile-example).

Problems solved by Avatar-CLI and surrounding practices:

- *Works on my machine* - With Avatar-CLI, each developer (and/or CI agent) gets
  a consistent and reproducible environment built with a combination of docker
  images.
- Avatar-CLI helps to fight
  [configuration drift](https://martinfowler.com/bliki/ConfigurationSynchronization.html).
  Tools and configurations in the CI/CD environments and developers'
  environments tend to accumulate differences and mismatches over time.
  Avatar-CLI allows using exactly the same tools, having a single source of
  truth for their configuration.

## Features

- Multiplatform: Linux and MacOs.
- Tools version pinning. 
- Ability to combine many docker images, no need to create a catch-all image.
- SSH-Agent integration.
- GPG-Agent Integration (only in Linux)
- JetBrains IDEs integration.
