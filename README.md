# System Program   
# Set Up
Start Apps(Y:)” drive\Subject\vm_image\EmbeddedSystem\EmbeddedSystem_2024A **ShortCut**

Open Putty 
Select `Serial` 
Serial line: `COM3`     
Speed: `115200`   

Connect to linux system  
```cd /mnt/nfs```   
``` mount -t nfs 192.168.1.1:/home/comp3438/arm-board /mnt/nfs -o nolock ```

# Step 1 Copy file
use firefox to download the file   

``` sudo bash```   
Password: 12345    
Copy helloworld_dirver.c to arm-board/linux-3.0.8/drivers/char  

```cd arm-board/linux/drivers/char```  
if the file is located at Desktop you can use the follow command to copy the file
```cp /home/comp3438/Desktop/helloworld_driver.c helloworld_driver.c```   
`cp /home/comp3438/Desktop/Kconfig Kconfig`   
`cp /home/comp3438/Desktop/Makefile Makefile`  

Maybe you need edit the Kconfig and Makefile the LED part

cd to ~/arm-board copy `helloworld_user.c`   
`cp /home/comp3438/Desktop/helloworld_user.c helloworld_user.c`

# Step 2 Makefile
`cd linux3.0.8`   
`make menuconfig`   
Get into menuconfig
Find DeviceDriver -> CharacterDriver -> Helloworld
Set `M`  Press Tap to switch the mode   
Then confirm

# Step 3 Compile User File

cd to `~/arm-board`   
`arm-linux-gcc helloworld_user.c -o helloworld_user`   

# Step 4 Putty
if you cannot find the file, you may try `cd ..` then `cd nfs` to refresh   
`cd linux-3.0.8/drivers/char`

Set the driver file the filename is **ko**   
`insmod helloworld_driver.ko`  
`cd /proc`   
`mknod /dev/helloworld c 250 1`   

then cd to `nfs`   
`./helloworld_user`   

# Remove device
`umount /mnt/nfs`

