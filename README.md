# dnuke
Ruby script for conveniently nuking Docker containers and volumes by name

## Introduction
The secondary purpose of this project is as follows: provide a quick and easy way for developers to remove Docker containers and volumes that fuzzily match an input / group of inputs. This is likely a niche purpose as it assumes that the developer has ruby installed on their machine, is working with Docker, is working on a project that utilizes similar naming conventions for their Docker containers / volumes, and also has a need to *remove* said containers and volumes often enough to justify the use of a script to do so. Which is exactly the kind of niche that I filled when I started developing dnuke.

The primary purpose of this project makes much more sense; to further my own personal learning. I wanted a personal project that would allow me to:
- Improve my skills with Ruby
- Familiarize myself with Docker
- See what it took to write a script executable from the command line
- Create something somewhat useful, even if it's only useful for myself or my coworkers
- Practice using `git` and GitHub
- Write documentation

#### Disclaimer
To clarify, dnuke doesn't do anything that Docker can't do better itself. Testing for dnuke is minimal / nonexistent.

If any of the features provided by this script sound appealing to you, I highly recommend that you check out the official Docker [documentation](https://docs.docker.com). [`docker system prune`](https://docs.docker.com/engine/reference/commandline/system_prune/) may be what you're looking for.

**Use at your own risk.**

## Requirements
coming soon&trade;

## Installation
coming soon&trade;

## Usage
Pass the name(s) of your containers / volumes to dnuke:

`dnuke project1`

Your output should look something like this:

```bash
$ dnuke project1

I, the mighty dnuke, was passed: project1

removing containers that match: project1
  container project1_web_1 was removed
  container project1_postgres_1 was removed

removing volumes that match: project1
  volume project1_postgres was removed

--------------------------------------------------------------------
```

You can pass multiple container / volume names as arguments:

```bash
$ dnuke project1 project2

I, the mighty dnuke, was passed: project1

removing containers that match: project1
  container project1_web_1 was removed
  container project1_postgres_1 was removed

removing volumes that match: project1
  volume project1_postgres was removed

--------------------------------------------------------------------

I, the mighty dnuke, was passed: project2

removing containers that match: project2
  container project2_web_1 was removed
  container project2_postgres_1 was removed

removing volumes that match: project2
  volume project2_postgres was removed

--------------------------------------------------------------------
```

dnuke uses fuzzy matching when searching your local Docker containers and volumes:

```bash
$ dnuke cat

I, the mighty dnuke, was passed: cat

removing containers that match: cat
  container caterpillar_web_1 was removed
  container caterpillar_postgres_1 was removed

removing volumes that match: cat
  volume caterpillar_postgres was removed

--------------------------------------------------------------------
```

If a container and / or volume isn't removed successfully, dnuke will notify you that there was an issue:

```bash
...

removing containers that match: project1
Error response from daemon: You cannot remove a running container a0123456789ba0123456789ba0123456789ba0123456789ba0123456789ba012. Stop the container before attempting removal or force remove
>>> there was an issue removing container project1_web_1 (a0123456789b)

removing volumes that match: project1
Error response from daemon: remove project1_postgres: volume is in use - [a0123456789ba0123456789ba0123456789ba0123456789ba0123456789ba012]
>>> there was an issue removing volume project1_postgres

--------------------------------------------------------------------
```

## TODO
- Expand functionality to encompass Docker images / networks (build caches?)
- Add flags to give the user options as to what they want to remove (or not remove)
