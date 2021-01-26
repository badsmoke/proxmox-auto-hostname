# proxmox-auto-hostname
change vm hostname automatic to vm-name

## what can it do?
the script fetches its vm-name via api and changes it to this one

for operating systems that use "cloud-init" you can simply put the script into the folder

`/var/lib/cloud/scripts/per-boot/` and it will be executed on every boot.

for all others you could also just create a cronjob
`@reboot /path/to/script/vm-boot.sh`


don't forget to make the script executable
`chmod +x vm-boot.sh`

a proxmox user must be created who has at least read rights to the api/vms

## how does it work

the script retrieves its vm-name with the help of the mac address and the proxmox api

first fetches the mac address from each interface
Then the script connects to the api of proxmox and goes through all clusters, vm and their network interface and compares the mac addresses with each other, if the mac addresses match the corresponding vm-name is chosen and set
