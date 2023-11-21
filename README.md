# ADXL-PI-KLIPPER
##No-Nonsense guide to ADXL installation and Configuration serves to encompass all ADXL types in order to be thorough in case a person wants to have different style accelerometers installed/used.

Information is pulled and compiled from https://www.klipper3d.org/Measuring_Resonances.html and https://www.klipper3d.org/RPi_microcontroller.html

First, SSH into your RPi

Run the following commands:




```
sudo apt update
sudo apt install python3-numpy python3-matplotlib libatlas-base-dev
```

then install NumPy in the Klipper environment

```
~/klippy-env/bin/pip install -v numpy
```

Go to your printer.cfg file and add the following

```
#########################################################
#########         ADXL Configurations          ##########
#########################################################
[mcu rpi]
serial: /tmp/klipper_host_mcu

[adxl345]
cs_pin: rpi:None

[resonance_tester]
accel_chip: adxl345
probe_points:
    #Choose one below specific to your printer
    #125, 125, 20 #for 250mm beds
    #150, 150, 20 #for 300mm beds
    #175, 175, 20 #for 350mm beds
```

Under probe_points:

For a 250mm bed use 125, 125,
For a 300mm bed use 150, 150,
For a 350mm bed use 175, 175,

Now to do some things needed to run and use the ADXL

ssh into your pi again.

Install the rc script

```
cd ~/klipper/
sudo cp ./scripts/klipper-mcu.service /etc/systemd/system/
sudo systemctl enable klipper-mcu.service
```

Now we need to build the micro-controller code:

```
cd ~/klipper/
make menuconfig
```

CHOOSE LINUX PROCESSES

<img width="575" alt="image" src="https://github.com/TheVoronModder/ADXL-PI-KLIPPER/assets/142328467/d3537b66-8e1e-4e1a-a089-6fc46f4d7911">

Hit ESCAPE, and Y or YES

then run

```
sudo service klipper stop
make flash
sudo service klipper start
```
## Enable SPI and I2C on RPi

SSH into your pi again.
Run this:
```
sudo raspi-config
```
You will be prompted for your password

choose 3 or whatever number is "Interface Options"

<img width="483" alt="image" src="https://github.com/TheVoronModder/ADXL-PI-KLIPPER/assets/142328467/8f6b08b7-71a3-4e4b-b3fb-3a67095973c6">

Then SPI and I2C

<img width="631" alt="image" src="https://github.com/TheVoronModder/ADXL-PI-KLIPPER/assets/142328467/50bf2b14-c3a2-44d4-880d-82f004a5227e">


You hit ENTER on your keyboard and choose YES hwen the pop up question asks if you would like the SPI interface to be enabled.

Same for the I2C

### Save and close out of SSH

If your running the LDO Input Shaper Kit Like Me we need to install the Linux GPIO Character Device - Binary

### SSH back into your Raspberry Pi

Run these commands:

```
sudo apt-get install gpiod
```

your done!

## Now, lets test if the Pi can detect your ADXL. 
Connect your ADXL to your pi.

The following images are for if you are using wires to connect your ADXL from the GPIO pins on a RPi.

Credit to https://www.klipper3d.org/Measuring_Resonances.html
![image](https://github.com/TheVoronModder/ADXL-PI-KLIPPER/assets/142328467/6325036d-41c4-41cc-8551-d520a706eb9c)

For a Raspberry Pi 4

![image](https://github.com/TheVoronModder/ADXL-PI-KLIPPER/assets/142328467/eeda2fcc-ab3d-414e-a26c-c100fadf5ea5)

## If you have the LDO input shaper kit like I do its quite easy to install. 














