# YC99T reload the firmware

Note: The operation base on Windows XP/ Windows 7/10 or above

## Main control board firmware writing

### File list of system

- x-load.KD
- x-load.KS
- mini_ubi.img
- u-boot.bin
- uImage
- ubi.img

### PC software

-  putty.exe
-  tftpd32.exe

## Firmware writing process

### Preparation

* YC99C-5T need an RS485 connection cable，recommend to use RS232-RS485 converter，RS232 end connect to PC，RS485 end connect to 99C-5T，99C-5T end the main board has a three pins connector, two of the pins are used for connection. Showed as photo below,

![](https://gitee.com/genyeem/doc/raw/master/202110091940673.png)

* Connect Rs485 wire to the J8 connector of 99T main board, meanwhile computer internet cable show be connect to 99T.

![](https://gitee.com/genyeem/doc/raw/master/202110091942178.png "Note: only connect two pins")

*Note: only connect two pins*

* Short the  J1 pins on main board

  ![](https://gitee.com/genyeem/doc/raw/master/202110091946694.png)

  

* Set computer internet IP as: 192.168.0.88
* **Close all the other serial port related software (very important!).** 

* See if the computer comport is not com1, then need to modify the file comport number.（00_serial_boot\serial_boot.bat）, below photo is an example of modify the com1 to com2 if computer use com 2 for the operation.

  ![](https://gitee.com/genyeem/doc/raw/master/202110091949959.png)

  

* **Setup putty software: create a new session. The setting as follow: (Comport was select according to the PC comport)**

![](https://gitee.com/genyeem/doc/raw/master/202110091952127.png)



## Write CPU

* **Open the ‘00_serial_boot\serial_boot.bat’ file when 99T is power up.**

  ![](https://gitee.com/genyeem/doc/raw/master/202110091959702.png)

  ![](https://gitee.com/genyeem/doc/raw/master/202110092000266.png)

  See as the snap shot below:

  ![](https://gitee.com/genyeem/doc/raw/master/202110092001711.png)

  Press ‘Enter’ key, turn off the 99T power, and then turn on. If not see the script show in the red block in the snap shot below, then need to repeat the turn off and turn on process.

  ![](https://gitee.com/genyeem/doc/raw/master/202110092001088.png)

  The data transfer process takes about 50 second.

   

  **Open ‘Putty software’ and select comport, click open. Press a few times of ‘ENTER’ until it show up script ‘Serial Recovery#”in the black windows, at the same time, start the tftp32. Both of the software has to be run simultaneously. Lacking any of them will cause failure at the write CPU operation.**

  ![](https://gitee.com/genyeem/doc/raw/master/202110092002790.png)

  

*  **Input the command to write CPU, format as follow,** 

  **upgrade_tftp [server IP] [Mother board IP] [ID]**

```
[Server IP]: Computer IP addresses. For example like the photo above 192.168.0.88
[Mother board IP]: can be set to 192.168.0.10 (Has set to the same network segment as server IP, the last digit can set it randomly without conflict with Server IP and smaller than 255)
[ID]:  Randomly set, for example 1 , 2, 33, (use as the mac address in the u-boot)

ID could be a 10 Decimal system or a Hexadecimal number, and the program will convert it automatically.
 For example： upgrade_tftp 192.168. 0.88 192.168. 0.10 23 
upgrade_tftp 192.168. 0.88 192.168. 0.10 0x65

```

Run **upgrade_tftp 192.168.0.88 192.168.0.10 33**, the write CPU progress will start automatically.

The overall process will last for about 5 mins. No human interruption is needed. After finish the process, the equipment will reboot automatically.

