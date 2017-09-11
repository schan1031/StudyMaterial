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
  # N is another file descriptor
```

***Other Examples***
```bash
2> 1 # stderr to filename 1
2>&1 # stderr to stdout
i>&j # file descriptor i to j
>&j  # default 1 to j
```

#### Command <
- Acccepts input form a file
- Redirection of stdin

#### Command | (Pipe)
- General purpose chaining tool
- More general than >

***Examples***
```bash
grep searchword <filename # search for search word, input filename
cat *.txt | sort | uniq > resultfile
  # Pipes output of previous command to next command
  # Prints all txt files, sorts, grabs unique, write to 'resultfile'
```

### Interpolation
- Syntax is `$(...)`
- `echo "My directory is $(...) ok?"`

### Exec
- Redirects stdin to file
- Allows for line by line reading

```bash
exec < data-file
read a1             # prints line 1
read a2             # prints line 2
```

### Alias
- Create a shorthand for a command
- Stored for user in ~/.bashrc
- Can unalias with `unalias`

```bash
alias la="ls -a"
unalias la
```

### Regex
  - `.` - Any character
  - `^` - Beginning of line
  - `$` - Line end
  - `[abc]` - any character inside the brackets
  - `[!abc]` - any character not in the brackets
  - `?` - None or exactly one repeat of previous character
  - `+` - One or several of previous character
  - `*` - None or several repeats of previous
  - `{m,n}` - Minimum of m to max n repeats

### Brace Exapnsion
- Converts lists into separate strings
```bash
$ mkdir /tmp/example{1,2,3} # Creates three files
$ mkdir /tmp/example1 /tmp/example2 /tmp/example3
```
