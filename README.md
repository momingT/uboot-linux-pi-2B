# uboot-linux-pi-2B
I want to use uboot booting a linux kernel on raspberry pi 2B, and both are based on public distributions.

# 树莓派引导顺序
  在SD卡上建立FAT32分区，并确保该分区目录下存在以下文件：
  1. bootcode.bin
  2. start.elf
        可能需要fixup.dat文件，来配置RAM的空间划分（GPU和CPU）。
  3. *.img
  
  1st. Soc内部烧录程序，用于挂载SD卡上FAT32分区，方便二级boot访问SD卡中的文件；
  2nd. bootcode.bin 读取start.elf文件，并启动GPU；
  3rd. GPU初始化硬件设备，初始化完成后，并通过fixup.dat配置RAM的分配;
  4th. 执行二进制文件，可以是Linux内核、uboot或者裸板程序。
      默认start.elf文件从SD卡分区读取kernel7.img文件到RAM中，然后跳转CPU执行。所以可以通过u-boot.bin文件名为kernel7.img
      或者在configs.txt文件中配置（目前未找到配置方法）。
    
