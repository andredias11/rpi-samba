Docker container that creates a SMB share.

## Running

```
version: '3'
services:
  smb:
    image: charlesmknox/rpi-samba:v2
    restart: always
    ports:
      - 137:137
      - 138:138
      - 139:139
      - 445:445
    hostname: parenthostname
    volumes:
      - /mnt/smbsharefolder:/share/data
    command: -u "user:password" -u "user2:password" -s "backup:/share/data:rw:user,user2"
```

This example will bind `smbd` to docker host ip address
and mount two directories on docker host to container.
Additionally, the supplied hostname will be used for the NetBIOS name.
Two users will be created and given various access to four shares.
Ommitting users from a share results in guest access.
The `public` share will have guest access and be browsable.

## Connecting
You'll want to expose enough ports to make the server discoverable.
The example above should be enough to get you moving.

Open Finder, then press âŒ˜K. Enter `smb://<docker_host_ip>`
and press `Connect`.
Enter login and password you supplied at the run stage.
