# dvc.api.open()

Opens a file <abbr>artifact</abbr> as a
[file object](https://docs.python.org/3.7/glossary.html#term-file-object). May
only be used as
[context manager](https://www.python.org/dev/peps/pep-0343/#context-managers-in-the-standard-library).

> This has similar uses as the `dvc get` and `dvc import` CLI commands.

## Signature

```py
open(path, repo=None, rev=None, remote=None, mode="r", encoding=None)
```

## Parameters

- **`path`** - used to specify the location of the target artifact within the
  source project in `repo`, relative to the project's root.

- `repo` - specifies the location of the source DVC project. Both HTTP and SSH
  protocols are supported for online Git repositories (e.g.
  `[user@]server:project.git`). `repo` can also be a local file system path to
  an "offline" project. If not supplied, this defaults to the current working
  directory.

- `rev` - (optional)
  [Git-revision](https://git-scm.com/book/en/v2/Git-Internals-Git-References)
  (such as a branch name, a tag, or a commit hash). `rev` only has an effect
  when a URL is supplied as parameter to `repo`. If not supplied, it uses the
  default Git revision, `HEAD`.

- `remote` - (optional) name of the [DVC remote](/doc/command-reference/remote)
  to fetch the target artifact from. If not supplied, the default project's
  remote is used.

- `mode` - (optional) mirrors the namesake parameter in builtin
  [`open()`](https://docs.python.org/3.7/library/functions.html#open). Defaults
  to `"r"` (read).

- `encoding` - (optional) used to decode contents to a string. Mirrors the
  namesake parameter in builtin `open()`. Defaults to `"utf-8"`.

## Example: read CSV file from an external DVC repository

```py
import csv
import dvc.api

with dvc.api.open(
  "data/rows.csv",
  repo="https://github.com/example/dvc-repository"
) as fd:
  reader = csv.reader(fd)
  for row in reader:
    # ... Process columns
```

> See also `dvc.api.read` for a more direct way to read the complete contents of
> a file <abbr>artifact</abbr>.