# Scratched

Lists the files that will be deleted from the Graham scratch folder on the 15th of the month. This utility offers the following advantages over running `cat /home/scratch_to_delete/$(whoami)`:


1. Depth: via the `--depth` flag, the number of subfolders listed can be easily controlled. This limits the printout to only the top-level directories, making it easier to digest the information. The `--ls` flag can be used to automatically set the depth to show only the immediate children of your filter (see below), although this may be slower for large scratched lists.

2. Filterable: The command takes `grep` filters to filter the list down to directories you care about. This is especially powerful combined with...

3. Various actions modes: Using `--delete` and `--touch`, you can automatically delete/touch all the files selected by your filter. This automatically updates your scratch list, so you won't see these files on future invocations of `scratched`. If you've made manual touches or deletions, you can register these with `scratched` by with `--update`. (`scratched` does not alter the official graham `scratch_to_delete` file, but maintains it's own version of the file in your `~/.cache` dir).


```
Usage: scratched [OPTIONS] [PATTERN]

List the files that will be deleted on the 15th of the month.

PATTERN is a regex filter applied to the file list BEFORE any command actions are
taken.

The command operates in one of a few modes:

- list:   List all file paths seperated by newlines. Default mode.
- ls:     Like list, but only display immediate children of the current or specified
          directory
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
    list, update, delete, and touch modes). Alternatively, in ls mode, an absolute or
    relative path

  -d NUM, --depth NUM
    The maximum file tree depth to display. e.g. -d 3 would print up to 3
    subdirectories: '/scratch/username/foo'

  --ls
    Display only paths that are immediate children of the current working directory.
    Directories listed are those containing files to be deleted. If PATTERN is given,
    it is interpreted as an absolute path (if it starts with `/`) at which to search,
    or a relative path to the current workig directory. Note that this cannot be
    combined with --update, --delete, or --touch. To restrict any of these operations
    to the current working directory, use --pwd.

  --pwd
    Adds the current working directory to the start of the filter.

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
