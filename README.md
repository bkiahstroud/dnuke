# dnuke
Ruby script for conveniently nuking Docker containers and volumes by name

### Usage
Pass the name(s) of your containers / volumes to dnuke:

`dnuke project1`

Your output should look something like this:

```bash
$ dnuke project1

I, the mighty dnuke, was passed: project1

removing containers that match: project1
container a0123456789b was removed
container b9876543210a was removed

removing volumes that match: project1
volume project1_postgres was removed

--------------------------------------------------------------------
```

You can pass multiple container / volume names as arguments:

```bash
$ dnuke project1 project2

I, the mighty dnuke, was passed: project1

removing containers that match: project1
container a0123456789b was removed
container b9876543210a was removed

removing volumes that match: project1
volume project1_postgres was removed

--------------------------------------------------------------------

I, the mighty dnuke, was passed: project2

removing containers that match: project2
container b9876543210a was removed
container a0123456789b was removed

removing volumes that match: project2
volume project2_postgres was removed

--------------------------------------------------------------------
```

dnuke uses fuzzy matching when searching your local Docker containers and volumes:

```bash
$ dnuke cat

I, the mighty dnuke, was passed: cat

...

removing volumes that match: cat
volume caterpillar_postgres was removed

--------------------------------------------------------------------
```
