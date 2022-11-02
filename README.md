# Scratched

Lists the files that will be deleted from the Graham scratch folder on the 15th of the month. This utility offers two main advantages over running `cat /home/scratch_to_delete/[username]`:

1. Updateable: by running the command with `--update`, a new `scratch_to_delete` file will be generated in your `~/.cache` dir. This file will exclude any scratch files already deleted or updated (via touch or otherwise).

2. Depth: via the `--depth` flag, the number of subfolders listed can be easily controlled. This limits the printout to only the top-level directories, making it easier to digest the information.


```
Usage: scratched [OPTIONS] [PATTERN]

List the files that will be deleted on the 15th of the month.

By default, the files listed in /home/scratch_to_delete/[username] are listed,
but an updated version of this list can be produced using the -u/--update flag.
Any files that have been deleted or updated (via touch or otherwise) will be
removed from the list

Options
=======
  PATTERN
    regex pattern to match

  -d NUM, --depth NUM
    The maximum file tree depth to display. e.g. -d 3 would print up to 3
    subdirectories: '/scratch/username/foo'

  -u, --update
    Generate an updated version of the scratch_to_delete list, excluding any
    files that have already been updated or deleted
```

