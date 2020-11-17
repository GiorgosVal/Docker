# Resources
Video on [udemy](https://www.udemy.com/course/docker-mastery/learn/lecture/7742916#overview)

Docker Engine [installation guide](https://docs.docker.com/engine/install/) (follow the instructions for your specific distribution)

Docker Compose [installation guide](https://docs.docker.com/compose/install/) (follow the instructions for your specific distribution)

# Tips
- Do not use pre-installed setups (e.g. Digital Ocean, Linode, etc)
- Do not do `sudo apt install docker.io`

# Docker Engine installation through script
Visit [get.docker.com](https://get.docker.com/). It'll show you a script with instructions.

Open a terminal and execute the commands of the instructions, like:
```console
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ sh get-docker.sh
```
## Add the user to the docker group
`docker` requires `root` in order to perform, so by default to execute commands you'll have to use `sudo`.

For ***some*** Linux distributions you can add the user to the docker group, so as not to have to do `sudo docker` every time you want to execute a command.

>**WARNING:** When you add a user to the `docker` group, you actually give that user the ability to run a docker container layer that could have root permissions on the host. Some Linux distributions won't work with this docker option, so you'll have to do `sudo` every time.

# Useful tools
## Bash completion
Bash completion is a set of scripts that enable auto completion for docker commands. To install it follow the [instructions](https://docs.docker.com/compose/completion/).

## Tilix
[Tilix](https://gnunn1.github.io/tilix-web/) is a GUI that emulates a text terminal and runs a shell.
## ohmyzsh
Try this https://github.com/ohmyzsh/ohmyzsh

## Other cool stuff for your terminal
https://www.bretfisher.com/shell/

# Bind mounts
The default paths for bind mounts are:
//TODO
> Note: Bind mounts work for code and (usually) databases

