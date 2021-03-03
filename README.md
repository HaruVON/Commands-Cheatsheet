# Commands-Cheatsheet
List of commands that I often use

## SMB Mount

```
sudo mount -t cifs -o username=swiftd.adm //<server name>/<dir> <path to dir to mount>
```
  
## IP Reset via DNS

```

```

## Check Systemd Services

```
journalctl -u service-name.service
journalctl -u service-name.service -b
journalctl -u service-name
```

Just use the journalctl command, as in:

```
journalctl -u service-name.service
```

Or, to see only log messages for the current boot:

```
journalctl -u service-name.service -b
```

For things named <something>.service, you can actually just use <something>, as in:

```
journalctl -u service-name
```

```
journalctl -u swag -n 100 --no-pager
```


```
grep -rnw <dir> -e 'pattern'
```
  
```
find [where to start searching from] [expression determines what to find] [-options] [what to find]
fine <dir to search from> -name:option for file name 'pattern'
```

## Change ownership of files

```
sudo chown -R user:group <dir>
```
-R - recursive
