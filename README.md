# Commands-Cheatsheet
List of commands that I often use

## Get Full Path of Script

```bash
path=$(dirname "$(readlink -f "$0")")
```

## SMB Mount

```bash
sudo mount -t cifs -o username=swiftd.adm //<server name>/<dir> <path to dir to mount>
```
  
## Networking

### Networking with RHEL

```bash
nmcli con add con-name "static-ens32" ifname ens32 type ethernet ip4 xxx.xxx.120.44/24 gw4 xxx.xxx.120.1
nmcli con mod "static-ens32" ipv4.dns "xxx.xxx.120.1,8.8.8.8"
nmcli con up "static-ens32" iface ens32
nmcli con show
nmcli con del ens32
```

### IP Reset via DNS

```bash
if sudo grep -q /etc/dhcp/dhclient.conf -e 'inerface "ens160" {\n\tsend host-name = gethostname();\n\tsend dhcp-requested-address 192.168.10.101;\n}';
then
  sudo dhclient -r -v && sudo dhclient -4 -d -v -cf /etc/dhcp/dhclient.conf ens16- && sudo reboot;
else
  sudo echo 'inerface "ens160" {\n\tsend host-name = gethostname();\n\tsend dhcp-requested-address 192.168.10.101;\n}' >> /etc/dhcp/dhclient.conf;
  sudo dhclient -r -v && sudo dhclient -4 -d -v -cf /etc/dhcp/dhclient.conf ens16- && sudo reboot;
fi
``` 

or 

```bash
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

```bash
journalctl -u service-name.service
journalctl -u service-name.service -b
journalctl -u service-name
```

Just use the journalctl command, as in:

```bash
journalctl -u service-name.service
```

Or, to see only log messages for the current boot:

```bash
journalctl -u service-name.service -b
```

For things named <something>.service, you can actually just use <something>, as in:

```bash
journalctl -u service-name
```

```bash
journalctl -u swag -n 100 --no-pager
```

## Just CLI Stuffs  

Run a command in the background and disown
```bash
ctrl-z
bg
disown
```
  
```bash
grep -rnw <dir> -e 'pattern'
```
  
```bash
find [where to start searching from] [expression determines what to find] [-options] [what to find]
find <dir to search from> -name:option for file name 'pattern'
find ./ -name 'example.txt'
```

## Change ownership of files

```bash
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

  ```python
  import re
  with open("U_CAN_Ubuntu_20-04_LTS_STIG_V1R1_Manual-xccdf.xml") as fin, open('output', 'w') as fout:
    for line in fin:
      matches = re.findall('idref=\"V-\d\d\d\d\d\d', line)
      fout.writelines(match + '\n' for match in matches)
  ```

## SSH
  
### Generate SSH key
  
  ```bash
  ssh-keygen -b 4096
  ```
  
### View SSH Key Size
  
  ```bash
  ssh-keygen -lf <path_to_public_key_file>
  ```
