# Dockerizer

We use new system based on docker and ahoy command tool.

## Docker Compose

We use docker-compose.yml with .env file.

### Custom values on docker-compose.override.yml

If we need add custom variables, for example to setup php memory_limit, we add environment variables on `docker-compose.override.yml` file.

Then set your variable values on `.env` file

#### PHP variables

Check [apache-php](https://github.com/keopx/docker-apache-php) image and read [README.md](https://github.com/keopx/docker-apache-php/blob/master/README.md)

## Ahoy

### Install

http://www.ahoycli.com/en/latest/

```bash
sudo wget -q https://github.com/ahoy-cli/ahoy/releases/download/2.0.0/ahoy-bin-`uname -s`-amd64 -O /usr/local/bin/ahoy && sudo chown $USER /usr/local/bin/ahoy && chmod +x /usr/local/bin/ahoy
```

#### Autocomplete

Then, (for homebrew) you’ll want to create a file at `/usr/local/etc/bash_completion.d/ahoy` with the following:

```bash
#! /bin/bash

: ${PROG:=$(basename ${BASH_SOURCE})}

_cli_bash_autocomplete() {
     local cur opts base
     COMPREPLY=()
     cur="${COMP_WORDS[COMP_CWORD]}"
     opts=$( ${COMP_WORDS[@]:0:$COMP_CWORD} --generate-bash-completion )
     COMPREPLY=( $(compgen -W "${opts}" -- ${cur}) )
     return 0
 }

 complete -F _cli_bash_autocomplete $PROG
 ```

#### Commands

| Command             | Description                                                                                                                    |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| bash                | Run bash into web service container.                                                                                           |
| blt                 | Run BLT commands in the web service container.                                                                                 |
| composer            | Run Composer commands in the web service container.                                                                            |
| deploy              | Deploy using ansistrano.                                                                                                       |
| destroy             | Stop and remove containers, networks, images, and destroy volumes.                                                             |
| down                | Stop and remove containers, networks, images, and volumes.                                                                     |
| drupal              | Run Drupal Console commands in the web service container.                                                                      |
| drush               | Run Drush commands in the web service container.                                                                               |
| logs                | Show logs                                                                                                                      |
| ps                  | List containers.                                                                                                               |
| restart             | Restart services.                                                                                                              |
| rsync-files-prod    | Run Drush rsync @site.prod @site.local files directory | rsync options after -- https://github.com/drush-ops/drush/issues/3491 |
| rsync-private-prod  | Run Drush rsync @site.prod @site.local private directory                                                                       |
| start               | Start services.                                                                                                                |
| stop                | Stop services.                                                                                                                 |
| sync-all-prod       | Synd DB and files from @site.prod to @site.local.                                                                              |
| sync-db-prod        | Run Drush sql:sync @site.prod @site.local.                                                                                     |
| traefik             | Start traefik                                                                                                                  |
| up                  | Create and start containers.                                                                                                   |
| init                | Initialize a new .ahoy.yml config file in the current directory.                                                               |


[.ahoy.yml](https://raw.githubusercontent.com/keopx/dockerizer/master/.ahoy.yml)

#### Example:

[examples.ahoy.yml](https://github.com/ahoy-cli/ahoy/blob/master/examples/examples.ahoy.yml)
