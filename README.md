# Proxmox-zombie-disk-detector (CEPH storage only)

These commands will help you find disks that are not connected to any VM. You need to run it on the Proxmox node.
Replace POOL_NAME with the name of your pool

**`for i in $(rbd ls POOL_NAME); do if ! grep -r "$i" /etc/pve/nodes/ > /dev/null; then echo POOL_NAME/$i; fi; done;`**

**Be careful. Don't trust the script output 100%. Check every disk!!!**

Example:  
![zombie-disk](https://user-images.githubusercontent.com/88323643/170447316-844c269a-d612-494d-a229-24e78188cc85.jpg)

There are no such VMs:  
![vm-list](https://user-images.githubusercontent.com/88323643/170447477-cad92491-5b8f-49c2-b708-231813c49fc8.jpg)

Then run the command:  
`rbd rm YOUR_POOL_NAME/DISK_NAME`

If the disk is protected from deletion, check the snapshots:
`rbd snap ls YOUR_POOL_NAME/DISK_NAME`

We need to remove the protection. In my case, the command looks like this:  
`rbd snap unprotect HDD/vm-102-disk-2@barcdaily191217100934`
