+++
title = "Getting Started"
weight = 1
+++

We'll see an example of how to setup a NodeJS project with Avatar-CLI.

First of all, enter into your project directory:
```bash
cd /home/username/project_dir
```

Second, we'll initialize a new Avatar-CLI project here:
```bash
avatar init
```

The previous command will create the directory `.avatar-cli`, and a file called
`Avatarfile` inside of it. We'll edit this file to specify the tools we want to
use in our project:

```yaml
---
avatarVersion: '0.18.1' # This is not relevant... for now
projectInternalId: v2ZmtbkGuVdvGwVE # You will see a different ID, don't modify it
images:
  node: # OCI/Docker Image name
    tags:
      14-buster: # OCI/Docker Image tag
        # These are the binaries that we'll make accessible throw Avatar-CLI.
        # Notice that they are under the '14-buster' key that represents a tag.
        binaries:
          node: {}
          npm: {}
```

Now we are ready to use the configured tools, we can do it by just typing the
following command:
```bash
avatar shell
```

This command will be more or less verbose (and take more or less time to run)
depending on whether the required OCI images are available or not in your
system. In general terms you can expect the first time to be a little bit slow,
but the next ones will be very fast.

Once this command is executed, we'll be inside a subshell that allows us to use
the configured version of NodeJS and NPM (in interactive and non-interactive
modes):

```
» node --version
v14.14.0
» npm --version
6.14.8
```

Now... what we did is great, but we can do better. `npm` relies on disk caches
to minimize the amount of utilized network bandwith, but if we do nothing about
it, these caches will be discarded because we are running it inside containers.

Luckily for us, we can modify our `Avatarfile` to fix the situation:

```yaml
avatarVersion: '0.18.1' # This is not relevant... for now
projectInternalId: v2ZmtbkGuVdvGwVE # You will see a different ID, don't modify it
images:
  node: # OCI/Docker Image name
    tags:
      14-buster: # OCI/Docker Image tag
        # These are the binaries that we'll make accessible throw Avatar-CLI.
        # Notice that they are under the '14-buster' key that represents a tag.
        binaries:
          node: {}
          npm: {}
        
        runConfig:
          env:
            # We tell npm via environment variable where to store its cache
            npm_config_cache: /caches/.npm
          envFromHost:
            # Irrelevant for the cache issue, but useful if you want to use your
            # npm credentials with the containerized tools.
            - NPM_TOKEN
          volumes:
            # We create a volume that will be used as cache by npm
            /caches/.npm: {}
```

With this new file, a new per-project volume cache will be created. This will
ensure that we don't use more network bandwith than what's really needed.

As a side note, we have plans to free you from this hassle and automate more
aspects of the process, but we are not there yet.
