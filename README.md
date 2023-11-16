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

You mustn't use the same filename for the source and the copressed files

## Extract substring using regex

```
cat file.txt
Hello
The number is 123.
to you
The number is 123.
Bye
```

I want to extract `123`

### grep

```
cat file.txt | grep -Po '(?<=The number is )\d+' | head -1
```

### sed

All those lines will do the same

```
sed -rn 's/.*The number is ([0-9]+).*/\1/p' file.txt | head -1
sed -rn '0,/.*The number is ([0-9]+).*/{s/.*The number is ([0-9]+).*/\1/p}' file.txt
sed -rn '0,/.*The number is ([0-9]+).*/{s//\1/p}' file.txt
```

`s//` means use the same regex as in the range match.

### awk

All those line will do the same

```
awk 'match($0,/The number is [0-9]+/) {print substr($0,RSTART+14,RLENGTH-14);exit}' file.txt
awk 'match($0,/The number is ([0-9]+)/,m) {print m[1];exit}' file.txt
```

### Check open ports

```
sudo lsof -i :80 -i :443
sudo apt install -y net-tools
sudo netstat -plan
```

### Run script as root at startup

Create the script in `/etc/init.d/scriptname.sh`

```
chmod 755 /etc/init.d/scriptname.sh
ln -s /etc/init.d/scriptname.sh /etc/rc2.d/S99scriptname.sh
```
