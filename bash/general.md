# Bash notes

### stdin, stdout, stderr

- ***stdin*** - 0, used when file needs to read input
- ***stdout*** - 1, used to print a standard out, normally with `printf`
- ***stderr*** - 2, used to print errors, normally with `fprintf`

***Redirect Examples***
```bash
cat < filename          # redirect stdin to filename
cat filename > fileout  # redirect stdout to fileout
cat filename 2> fileerr # redirect stderr to fileerr if error
```
