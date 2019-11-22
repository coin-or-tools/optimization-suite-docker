This is a Docker image containing an installed version of the [COIN-OR
Optimization Suite](https://github.com/coin-or/COIN-OR-OptimizationSuite).

# Install and Use From Docker Hub

This image is now on [Docker
Hub](https://hub.docker.com/r/tkralphs/optimization-suite-docker/). To use,
simply install Docker (see instructions below) and then do

```
docker pull tkralphs/optimization-suite-docker
```

This retrieves a docker image containing the COIN-OR Optimization Suite. Once
you have the image, you can create a container, which is a running version of
the image. Note that this container is completely isolated from the OS you are
working in, so to run any useful commands inside it, you need to first copy
the files in to the container, then copy the results back out. To do this,
first create and start a container, as follows:

```
docker create --name=coin-or -it tkralphs/optimization-suite-docker
docker start coin-or
```

Now copy in any files you need:

```
docker cp example.mps coin-or:/tmp
```

Here, we are copying into the `/tmp` directory inside the container. Finally,
execute a solver command.

```
docker /var/coin-or/bin/cbc /tmp/example.mps > /tmp/output
```

and finally, copy the output back out

```
docker cp coin-or:/tmp/output .
```

Note that you are as root by default inside the container, but this is not
much of a risk inside a docker container, since it can be recreated easily.

# Build from Source

## Linux

Just clone the repository and build the docker image by

```
git clone https://github.com/tkralphs/optimization-suite-docker
cd optimization-suite-docker
sudo docker build -t optimization-suite image/
```

Now follow the instructions for running a solver from above, but note that all
commands will have to be executed with `sudo`.

## Windows

First install Docker for Windows. Depending on whether you are using a recent
version of Windows, you may need to enable virtualization in the BIOS
settings. For details, see

https://docs.docker.com/engine/installation/windows

As of this writing, it's important that you let Docker install Git for Windows
(do not uncheck the box for installing git in the installer, even though it
indicates that it is optional). After installing, run the "Docker Quickstart
Terminal" application. Make a note of the IP address assigned to the docker
machine (something like 192.168.99.100).

From the terminal clone the repository and build the docker image by the
commands

```
git clone https://github.com/PatWie/optimization-suite-docker
cd optimization-suite-docker
docker build -t optimization-suite image/
```

Finally, follow the instructions for running a solver from above.

## Mac OSX

Since Docker is a bit more difficult to get running on OSX than on Linux, this
is some additional documentation for the OSX crowd. OSX is not like
Linux---virtualization is not built into the kernel. Therefore, we need to run
the docker machine inside another VM. For this, we need virtualbox. The
instructions below are for installing virutalbox with `homebrew`, which seems
to work very well. (Caveat: I first found some old instructions on how to do
this and took a round-about path to the installation. Therefore, the list of
commands below is not exactly what I did. However, I think it's the right
incantation if you're starting from scratch with an updated install of
homebrew.)

Update: There now seems to be a trouble-free installation of Docker on OS X as
a native app. I haven't tried this, but I guess it should work well and might
be preferable is you are not already using `homebrew`.

First, install virtualbox

```
brew update
brew tap caskroom/cask
brew cask install virtualbox
```

Now install `docker` and `docker-machine`

```
brew install docker
brew install docker-machine
```

Create a new docker server to run in virtualbox and set environment variables
so docker knows how to connect to it.

```
docker-machine create --driver virtualbox default
eval "$(docker-machine env default)"
```

Now follow instructions as above for building the container

```
git clone https://github.com/tkralphs/optimization-suite-docker
cd optimization-suite-docker/
docker build -t optimization-suite image/
```

Finally, start up the server and the container

```
docker-machine start default
```

Now follow the instructions for running a solver from above.
