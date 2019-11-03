# 在linux宿主机中利用libvirt和qemu配置ubuntu虚拟机

``` bash 

# virt install
sudo virt-install --virt-type=kvm --name whisk1 --ram 4096 --vcpus=4 --os-variant=ubuntu14.04 --location=/var/lib/libvirt/boot/ubuntu14.iso --network=default,model=virtio --disk path=/var/lib/libvirt/images/ubuntu14_1.qcow2,size=40,bus=virtio,format=qcow2 --nographics --extra-args "console=ttyS0" -v

# virt clone
sudo virt-clone --original couchdb16 --name whisk4  --file /var/lib/libvirt/images/ubuntu16_4.qcow2 --auto-clone -m 52:54:00:6d:c6:87

# get MAC address
sudo virsh dumpxml VM_NAME | grep "mac address" | awk -F\' '{ print $2}'
# get ip address
arp -an |grep 52:54:00:4c:d1:70

# ssh tunnel - port forwarding
ssh -NfL5984:127.0.0.1:5984 whisk@couch16

# 调整qcow2磁盘大小
sudo qemu-img resize ubuntu16_04_40.qcow2 +30G

# 在guest vm上
sudo apt-get install lvm2
sudo fdisk -l
# 查看是否有变化,如果没有,reboot一下
sudo fdisk /dev/vda
# m - help
# n - new(maybe)
# d - delete
# t - type
# 8e - LVM
# w - write and save

ls /dev/vda*
sudo pvcreate /dev/vda4 # sudo pvresie --setphysicalvolumesize 70G /dev/vda4
sudo pvs
sudo vgcreate VolGroup00 /dev/vda4
sudo lvcreate -L 30G -n lvstuff1 VolGroup00 # sudo lvresize -L +40G /dev/VolGroup00/lvstuff1
sudo lvs
sudo lvextend -l +100%FREE /dev/VolGroup00/lvstuff1
sudo mkfs -t ext3 /dev/VolGroup00/lvstuff1
sudo mount -t ext3 /dev/VolGroup00/lvstuff1 llvm-install
sudo chown -R zevin:zevin llvm-install
```
