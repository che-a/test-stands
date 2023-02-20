**Гипервизор** – специальное программное обеспечение, которое позволяет создавать виртуальные машины и управлять ими;

* **Виртуальная машина** (далее VM) – это система, представляющая собой логический сервер внутри физического со своим набором характеристик, накопителями и операционной системой;
* **Хост виртуализации** — физический сервер с запущенным на нем гипервизором.

```
virt-install --name windows --ram 2048 --vcpus=2 
--os-type=windows --os-variant=winxp 
--disk path=/var/lib/libvirt/img/pc_smartvideo_nvr.qcow2,bus=virtio --network bridge=br0,model=virtio --graphics vnc,listen=0.0.0.0 --noautoconsole --autostart --boot cdrom,hd --disk device=cdrom,path="/var/lib/libvirt/iso/virtio-win-0.1.141.iso"
```

```
virt-install --name windows --ram 2048 --vcpus=1 --os-type=windows --os-variant=winxp --disk path=/var/lib/libvirt/img/pc_smartvideo_nvr.qcow2,bus=ide --graphics vnc,listen=0.0.0.0 --noautoconsole --autostart --boot hd 
```
