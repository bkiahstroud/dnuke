# dnuke
Ruby script for conveniently nuking Docker containers and volumes by name

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
