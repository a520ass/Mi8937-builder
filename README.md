# Image Builder
Image builder for Mi8937

进入原厂的fastboot安装lk2nd到boot
https://github.com/msm8916-mainline/lk2nd/releases/download/22.0/lk2nd-msm8952.img  
fastboot flash boot lk2nd-msm8952.img

安装后重启到lk2nd 的fastboot里（开机时按住 音量下键）  
若原厂 bootloader 也用相同按键：  
❌ 不要开机瞬间按（会触发原厂 fastboot）  
✅ 等屏幕亮 / 设备振动后再按（让原厂 BL 忽略按键，交给 lk2nd 处理）  

再刷ubuntu 的 boot system  
fastboot flash boot boot.bin  
fastboot flash system rootfs.bin  

=================================================

boot.bin 里面默认是红米3s的dtb，如果是其它mi8937设备，需要自行修改boot.bin里面的extlinux.conf 的dtb名称，修改方法如下：  
simg2img boot.bin bootext.bin  
mkdir -p /mnt/boot  
mount bootext.bin /mnt/boot  
挂载后修改/mnt/boot/extlinux/extlinux.conf，修改完成后umount /mnt/boot  
img2simg bootext.bin bootnew.bin  
使用fastboot刷入bootnew.bin即可  
