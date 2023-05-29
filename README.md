# Bash Tricks

## Check if a user can run sudo

```
try_sudo=$(sudo -nv 2>&1); test -z "$try_sudo" || echo "$try_sudo" | grep -q assword
```

Will return 0 if the user is allowed to use `sudo` and 1 otherwise.

Idea is from <https://superuser.com/a/1183480/1747454>.

## Compress pdf file

```
ps2pdf -dPDFSETTINGS=/ebook source.pdf compressed.pdf
```
