# Commands-Cheatsheet
List of commands that I often use

## SMB Mount

```
sudo mount -t cifs -o username=swiftd.adm //<server name>/<dir> <path to dir to mount>
```
  
## IP Reset via DNS

```
if sudo grep -q /etc/dhcp/dhclient.conf -e 'inerface "ens160" {\n\tsend host-name = gethostname();\n\tsend dhcp-requested-address 192.168.10.101;\n}';
then
  sudo dhclient -r -v && sudo dhclient -4 -d -v -cf /etc/dhcp/dhclient.conf ens16- && sudo reboot;
else
  sudo echo 'inerface "ens160" {\n\tsend host-name = gethostname();\n\tsend dhcp-requested-address 192.168.10.101;\n}' >> /etc/dhcp/dhclient.conf;
  sudo dhclient -r -v && sudo dhclient -4 -d -v -cf /etc/dhcp/dhclient.conf ens16- && sudo reboot;
fi
``` 

or 

```
if ! sudo grep -q /etc/dhcp/dhclient.conf -e 'inerface "ens160" {\n\tsend host-name = gethostname();\n\tsend dhcp-requested-address 192.168.10.101;\n}';
then
  sudo echo 'inerface "ens160" {\n\tsend host-name = gethostname();\n\tsend dhcp-requested-address 192.168.10.101;\n}' >> /etc/dhcp/dhclient.conf;
fi

sudo dhclient -r -v && sudo dhclient -4 -d -v -cf /etc/dhcp/dhclient.conf ens16- && sudo reboot;
``` 

## Systemd Services

systemctl commands:

- **enable**: enables on boot
- **status**: gets status
- **restart**
- **start**
- **reload**

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

## Just CLI Stuffs  

Run a command in the background and disown
```
ctrl-z
bg
disown
```
  
```
grep -rnw <dir> -e 'pattern'
```
  
```
find [where to start searching from] [expression determines what to find] [-options] [what to find]
find <dir to search from> -name:option for file name 'pattern'
find ./ -name 'example.txt'
```

## Change ownership of files

```
sudo chown -R user:group <dir>
```
-R - recursive

# Documentation

## Ansible

### Vars
- https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html
  
## OSCAP
  
### Link
- https://community.tenable.com/s/question/0D5f200006Ec9SGCAZ/disa-stig-against-centos

## Python

  ```
  import re
  with open("U_CAN_Ubuntu_20-04_LTS_STIG_V1R1_Manual-xccdf.xml") as fin, open('output', 'w') as fout:
    for line in fin:
      matches = re.findall('idref=\"V-\d\d\d\d\d\d', line)
      fout.writelines(match + '\n' for match in matches)
  ```
