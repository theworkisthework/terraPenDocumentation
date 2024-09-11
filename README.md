# terraPen Documentation

This GitHub repo is the source for the [terraPen documentation site](https://theworkisthework.github.io/terraPenDocumentation/).

The repo uses GitHub actions to automatically build and publish the site when a commit is puched or applied via Pull Request to the main branch.

The live site is in the **gh-pages** branch, which is hosted using GitHub pages.  You should not modify content in the gh-pages branch directly, this branch should only be written to by the GitHub action configured on the repository (see the .github folder checked into the repository main branch).

## Adding content

The documentation is written using Markdown, which is then transformed into a static web site by a tool called [MkDocs](https://www.mkdocs.org).  The site is styled using [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).  This extends basic Markdown to offer more advanced page layout and features.

Refer to the [MkDocs](https://www.mkdocs.org) and [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) documentation to learn how to configure the site and make use of advanced features.

## Spell checking

When the site is built using the GitHub action a [spell check](https://cspell.org) is run (using UK English dictionary).  If there are words that fail the spell check, but are valid words, it is possible to extend the spell checking dictionary using a page specific addition or a site wide configuration.

### Add site wide additional words

To add a word to the spell check dictionary you need to edit the file **cspell.json** in the root directory of the repository. Add the word to the **words** array.  The new word should be in double quotes (") and there must be a comma after the previous word.

### Adding page specific words

If you have some words that are unique to a specific page and there is no need to add them to the site wide dictionary, then you can add a directive to the top of a page to add additional words for the current page.  This annotation will not be visible in the rendered web site.

The annotation should look like this:

```
<!--- cSpell:ignore terraPen gcode -->
```

The format is a space separated list of words following the **cSpell:ignore** directive, within a markdown comment (`<!--- -->`)

## Link Checking

In addition to spell checking, all links within the site are also [checked](https://linkchecker.github.io/linkchecker/) to ensure the site doesn't contain broken links.

There are sometime errors or warnings you want the link checker to ignore.  These rules can be configured in the **linkcheckerrc** file in the root directory of the repo.  Details of how to configure the link checker can be found in the [documentation](https://linkchecker.github.io/linkchecker/).

## Running the build locally

You should run the build locally before creating a pull request.  The local build will highlight any issues with the changes you are about to commit. There are 3 ways to work locally:

- Install all the tools on your system
- Use a container using [Podman](https://podman.io/)
- Use a container using [Docker](https://www.docker.com)

### Containers on MacOS and native Windows

Containers are a great way to share environments without having to install, configure and maintain software on a system.  The container can be built then used wherever the software is needed.  However, containers typically need a Linux system to run.  Unlike a virtual machines, containers are lightweight as they share the Linux kernel of the host system, so a full operating system doesn't need to be booted when a container is started.

This is an issue as neither native Windows or MacOS are Linux systems, so to get containers running on these platforms Podman and Docker run a Linux virtual machine in the background where the containers actually run.  The desktop also introduces additional restrictions regarding how running containers can access local files.  You typically need to use directories within your home directory for running containers to be able to access files.

It is recommended that Windows users use Windows Subsystem for Linux (WSL) and run all podman or docker commands in a Linux WSL terminal.  MacOS users will need to run the virtual machine.  There are desktop application to make it easier to manage the virtual machine environment.  Podman is free for all users, Docker charges for commercial use of the Docker Desktop application, the commandline, non-virtualised (Linux native) docker engine is free to use.

Linux and Windows Subsystem for Linux can run containers without having the additional virtual machine running.

### Local install

The build system uses a Unix style script to execute the required commands.  Linux and MacOS systems are Unix based systems and the standard terminal applications are able to run the build script.  Windows users will need to use the Windows Subsystem for Linux to provide a Linux terminal to run the script.

You need to ensure you have the necessary software installed on your system, the examples below will show Linux, Ubuntu 24.04 LTS instructions.  You will need to modify as needed for your own environment (MacOS users can use [Homebrew](https://brew.sh) to do the installations)

Steps to installed required packages on Ubuntu Linux using the terminal (command line):

1. Update the package catalog and updating to latest packages - `sudo apt-get update -y && sudo apt-get upgrade -y`
2. Install the required base packages for MkDocs and the extensions - `sudo apt install -y build-essential python3-dev python3-pip python3-setuptools python3-wheel python3-cffi libcairo2 libpango-1.0-0 libpangocairo-1.0-0 libgdk-pixbuf2.0-0 libffi-dev shared-mime-info nodejs npm`
3. Configure the system to map the python command to the python3 command.
    1. Ensure you are in your home directory, running the cd command with no paramters will do this `cd`
    2. Modify the .bashrc file `nano .bashrc`
    3. Add a line to the file `alias python=python3`
    4. Save the changes `Ctrl+o` confirm the filename by pressing enter key
    5. Leave the editor `Ctrl+x`
    6. Make the change live using command `source .bashrc`
4. Change to the directory where you want the cloned repo to be placed `cd ....`
5. Clone the repository, if not already cloned to your local system `git clone https://github.com/theworkisthework/terraPenDocumentation.git`
6. Change to the repo directory `cd terraPenDocumentation`
7. Install the python dependencies `pip install -r requirements.txt`
8. Install the Node.js dependencies `npm install`

You now have the environment needed to work locally to build and test MkDocs on your system.

To run a local build you need to be in the repo base directory on your local system, then run command `./build.sh`.  This will build the site into the **public** directory, then run a spell check and linkchecker.  You should resolve any errors before commiting changes to git.

To develop content you can run a test server, which will automatically update as you modify and save files.  To start the test server run command `mkdocs serve` then open a browser to address [http://localhost:8000](http://localhost:8000).  When you have finished you can stop the server using **Ctrl+c**

### Podman

[Podman](https://podman.io/) is software that lets you run containers on your local machine.  It is open source and free to use and available on Windows, Linux and MacOS.

Windows users should use Windows Subsystem for Linux (WSL), MacOS users need to use Podman machine to host a virtual Linux machine, so the Podman Desktop application is recommended to make managing the VM easier.  The Podman VM must be running before any podman commands can be issued on MacOS.

Linux / WSL users can usually install podman with command `sudo apt install -y podman`, different distros may use a different package manager, if so you will need to lookup the appropriate command for your Linux distro.

Before you can run the container it needs to be built.  The Dockerfile in the dev directory contains the definition of the container needed to build and test the documentation in the repo.

To build the container image you must be in a terminal session in the root of the cloned github repository, then issue command:

```bash
podman build -t mkdocs-build -f ./dev/Dockerfile .
```

You can verify if the image has been build with command `podman images `.  You should see output similar to :

```text
REPOSITORY                           TAG         IMAGE ID      CREATED        SIZE
localhost/mkdocs-build               latest      b07c14f6d5a7  6 minutes ago  289 MB
docker.io/squidfunk/mkdocs-material  9.5.34      3766f5ea33a9  10 days ago    205 MB
```

**localhost/mkdocs-build** is the container that contains the tooling we need.

To build the site and run the spell and link checker tooling run the command from the root directory of the repo clone:

```bash
podman run -it --rm --name mkdocs-build -v `pwd`:/site --entrypoint /site/build.sh mkdocs-build
```

To run the test server so you can check formatting whilst editing the markdown files run command:

```bash
podman run -it --rm --name mkdocs-serve -p 8000:8000 -v `pwd`:/site mkdocs-build
```

This will start a web server that will update content everytime a markdown file is saved, so you get automatic page update.  To see the site open a browser to [http://localhost:8000](http://localhost:8000).  When you have finished you can terminate the server by pressing **Ctrl+c**

The podman commands are quite complex to remember, so if you have nodeJS and npm installed (`sudo apt install -u nodejs npm`) then you can use the npm commands:

- `npm run podman-build-image`
- `npm run podman-build`
- `npm run podman-serve`

to run the corresponding podman command, again these need to be run the root directory of the repo clone.

### Docker

Docker is another program that allows you to run containers on your local machine.  Unlike Podman there are some commercial restrictions and you may be required to purchase a license to use Docker on your system, refer to the [Docker site](https://www.docker.com) for details.

To install docker on Linux or WSL follow the instructions for [Docker Engine](https://docs.docker.com/engine/install/), be sure to follow the post install instructions too - including adding your user to the docker group.  For MacOS follow instructions for [Docker Desktop](https://docs.docker.com/desktop/install/mac-install/)

Before you can run the container it needs to be built.  The Dockerfile in the dev directory contains the definition of the container needed to build and test the documentation in the repo.

To build the container image you must be in a terminal session in the root of the cloned github repository, then issue command:

```bash
docker build -t mkdocs-build -f ./dev/Dockerfile .
```

You can verify if the image has been build with command `docker images`.  You should see output similar to :

```text
REPOSITORY     TAG       IMAGE ID       CREATED             SIZE
<none>         <none>    e963c1c8a27d   About an hour ago   258MB
mkdocs-build   latest    24157cd923dc   About an hour ago   258MB
```

**mkdocs-build** is the container that contains the tooling we need.

To build the site and run the spell and link checker tooling run the command from the root directory of the repo clone:

```bash
docker run -it --rm --name mkdocs-build -v `pwd`:/site --entrypoint /site/build.sh mkdocs-build
```

To run the test server so you can check formatting whilst editing the markdown files run command:

```bash
docker run -it --rm --name mkdocs-serve -p 8000:8000 -v `pwd``:/site mkdocs-build
```

This will start a web server that will update content everytime a markdown file is saved, so you get automatic page update.  To see the site open a browser to [http://localhost:8000](http://localhost:8000).  When you have finished you can terminate the server by pressing **Ctrl+c**

The docker commands are quite complex to remember, so if you have nodeJS and npm installed (`sudo apt install -u nodejs npm`) then you can use the npm commands:

- `npm run docker-build-image`
- `npm run docker-build`
- `npm run docker-serve`

to run the corresponding docker command, again these need to be run the root directory of the repo clone.