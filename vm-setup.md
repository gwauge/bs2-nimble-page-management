## NVRAM VM setup guide

1. create backing storage files for each nvdimm, e.g.: 
```console
touch nvdimm0 nvdimm1
```

2. create QEMU image inside appropriate folder
```console
sudo qemu-img create -f qcow2 /var/lib/libvirt/images/ubuntu22.qcow2  20G
```

3. configure provided XML file `ubuntu22.xml`
   1. specify path to distribution ISO file under `<devices> > <disk> > <source> > file`
   2. specify path to backing storage file defined in step 1 under `<memory> > <source> > <path>`
   3. configure machine to your liking

4. create VM
```console
virsh create ubuntu22.xml
```

5. connect to VM (for example using `virt-manager`) & install OS

6. upon request, eject installation media
```console
virsh change-media ubuntu22 sda --eject
```

7. shutdown VM

8. edit VM config through
```console
virsh edit ubuntu22
```

9. change boot order under `<os>`, so that `hd` is above `cdrom` or remove `cdrom` entirely

10. start your VM. everything should work as expected!