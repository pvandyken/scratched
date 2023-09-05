# Scratched

Lists the files that will be deleted from the Graham scratch folder on the 15th of the month. This utility offers two main advantages over running `cat /home/scratch_to_delete/[username]`:

1. Updateable: by running the command with `--update`, a new `scratch_to_delete` file will be generated in your `~/.cache` dir. This file will exclude any scratch files already deleted or updated (via touch or otherwise).

2. Depth: via the `--depth` flag, the number of subfolders listed can be easily controlled. This limits the printout to only the top-level directories, making it easier to digest the information.


```
Usage: scratched [OPTIONS] [PATTERN]

List the files that will be deleted on the 15th of the month.

PATTERN is a regex filter applied to the file list BEFORE any command actions are
taken.

The command operates in one of a few modes:

- list:   List all file paths seperated by newlines. Default mode.
- update: Update the `scratch_to_delete` list. Files already deleted or touched more
          recently than the deadline are removed from the list. Activated using
          -u/--update.
- delete: Delete all files. Activated using --delete
- touch:  Touch all files that currently exist. Files that have already been deleted
          are ignored. Activated using --touch

Finally, `scratched` has a `--check` mode that exits 0 if the official
`scratch_to_delete` file is newer than the local cache. This is useful for a
`.bashrc` file check:

  if scratched --check; then
    >&2 echo "scratch_to_delete has been updated"
  fi

Options
=======
  PATTERN
    Regex path filter. scratched only acts on files kept by the filter (including
    list, update, delete, and touch modes)

  -d NUM, --depth NUM
    The maximum file tree depth to display. e.g. -d 3 would print up to 3
    subdirectories: '/scratch/username/foo'

  --ls
    Automatically determine the depth so that only the immediate children of directories
    selected by PATTERN are shown. If no PATTERN is given, then only immediate children
    of the top scratch directory are printed    

  -u, --update
    Generate an updated version of the scratch_to_delete list, excluding any
    files that have already been updated or deleted. For long scratched lists, this
    operation can take a very long time; it is therefore recommended to pre-filter the
    filelist using PATTERN.

  --delete
    Delete all files selected by the filter

  --touch
    Touch all files selected by the filter that currently exist

  --check
    Check if the official `scratch_to_delete` file on graham has been updated compared
    to the local cached version.
```

## Installation

Easiest option is through `pipx`:

```bash
pipx install git+https://github.com/pvandyken/scratched.git
```

`pipx` installation instructions found [here](https://pypa.github.io/pipx/installation/). Note that the python packaging is just to make installation easier; the actual code is pure bash.
