# Bash notes

### stdin, stdout, stderr

- ***stdin*** - 0, used when file needs to read input
- ***stdout*** - 1, used to print a standard out, normally with `printf`
- ***stderr*** - 2, used to print errors, normally with `fprintf`

***Examples***
```bash
cat < filename          # redirect stdin to filename
cat filename > fileout  # redirect stdout to fileout, > defaults to 1
cat filename 2> fileerr # redirect stderr to fileerr if error
```

### Redirection

#### Command >
- Redirects stdout to a file
- Creates a file if not present, or overwrites if present

#### Command >>
- Redirect stdout to file
- Appends to existing file, or creates if doesn't existing

***Examples***
```bash
: > filename
  # : serves as placeholder, has no output
  # replaces filename, or creates it with 0 length, same as 'touch'

1> filename
  # Redirects stdout to 'filename'

1>> filename
  # Redirects and appends stdout to 'filename'

&> filename
  # Redirects both stdout and stderr to 'filename'

M> N
  # M is file descriptor, defaults to 1 or stdout
  # N is a filename

M>&N
  # N is another file descriptor, e.g. 2>&1
```
