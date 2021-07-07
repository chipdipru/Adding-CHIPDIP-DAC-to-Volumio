# Adding-CHIPDIP-DAC-to-Volumio
Adding new DAC to Volumio

1) Copy files «GenericI2SDACMaster.dtbo» and «RasGPIOCtrl_v5»  to “overlays” folder on SD-card with Volumio. GenericI2SDACMaster.dtbo is an overlay for I2S master DAC. RasGPIOCtrl_v5 is software for controlling Raspberry GPIOs.

2) Insert SD card into Raspberry and boot up. Activate SSH. To do it, in your browser go to http://VolumioIPAddress/dev/ , find SSH and clock ENABLE. Then reboot.

3) Connect to your  Raspberry via SSH (for example by means of Putty utility).

4) Copy file «RasGPIOCtrl_v5» to /home/volumio

cp /boot/overlays/./RasGPIOCtrl_v5 /home/volumio/./RasGPIOCtrl_v5

Check the file has been copied.

ls -al /home/volumio

File «RasGPIOCtrl_v5» should be on the shown list.

5) Set access rights for file «RasGPIOCtrl_v5».

chmod +x ./RasGPIOCtrl_v5

6) Make software «RasGPIOCtrl_v5» start automatically at Raspberry boot. 
Open file /etc/rc.local.

sudo nano /etc/rc.local

In the file before string “exit 0” add string

/home/volumio/./RasGPIOCtrl_v5 &

Press Ctrl+X for exit, then press Y to save modifications, then press Enter.

7) To add new DAC open file dacs.json.

sudo nano /volumio/app/plugins/system_controller/i2s_dacs/dacs.json

In the file add the following string in DAC list.

{"id":"chipdip-master-dac","name":"CHIPDIP Master DAC","overlay":"GenericI2SDACMaster","alsanum":"2","mixer":"","modules":"","script":"","needsreboot":"yes"}

Press Ctrl+X for exit, then press Y to save modifications, then press Enter.

8) Then reboot Raspberry.

reboot

9) In Volumio menu from DAC list choose "CHIPDIP Master DAC" and reboot Raspberry.

Raspberry GPIOs used

Resolution	 RES0	  RES1

       16   	0   	0
       24   	1   	0
       32   	0   	1


Frequency, kHz  SR0,   SR1,   SR2,

           44,1	  0	   0	  0
            48	  1	   0	  0
           88,2	  0	   1	  1
            96	  0	   1	  0
          176,4	  1	   1	  1
           192	  1	   1	  0

