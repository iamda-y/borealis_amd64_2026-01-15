# Lorem ipsum
blah blah blah

## Limitations:

-
-
-

## Instructions:

- Download and extract the latest Release contents
- Launch a crosh-spawned shell and run the commands

### Contents:

- `lsb-release`
- `dlc_metadata.json`
- `vm_kernel`
- `vm_rootfs.img`

### Commands:

- Prerequisites
```sh
sudo truncate -s 0 /var/log/update_engine.log                                           # clear logs
sudo dlcservice_util --uninstall --id="borealis-dlc"                                    # uninstall
cat /etc/lsb-release && dlc_metadata_util --get --id="borealis-dlc"                     # pre-compare
sudo initctl stop update-engine                                                         # pre-spoof 
sudo initctl stop dlcservice                                                            # pre-spoof
sudo mount --bind /path/to/lsb-release /etc/lsb-release                                 # spoof
sudo dlc_metadata_util --set --id="borealis-dlc" --file="/path/to/dlc_metadata.json"    # spoof
sudo initctl start update-engine                                                        # post-spoof
sudo initctl start dlcservice                                                           # post-spoof
cat /etc/lsb-release && dlc_metadata_util --get --id="borealis-dlc"                     # post-compare
sudo dlcservice_util --install --id="borealis-dlc"                                      # install
cat /var/log/update_engine.log                                                          # check logs
```
- Installation
```sh
# Creates the vmc
vmc start \
  --no-shell \
  --no-start-lxd \
  --writable-rootfs \
  --vm-type="CROSTINI" \
  --kernel="/path/to/vm_kernel" \
  --rootfs="/path/to/vm_rootfs.img" \
borealis
```
- Postrequisites
```sh
# Launch a root shell and set a root password inside the guest
vsh --vm_name=borealis --owner_id=${CROS_USER_ID_HASH} --user=root
[root@Chromebook ~]# passwd root
```
- Usage
```sh
# TODO
```
- Credits
```sh
# TODO
```
