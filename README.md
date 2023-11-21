# ADXL-PI-KLIPPER
No-Nonsense guide to ADXL installation and Configuration

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
[mcu rpi]
serial: /tmp/klipper_host_mcu

[adxl345]
cs_pin: rpi:None

[resonance_tester]
accel_chip: adxl345
probe_points:
    100, 100, 20  # an example
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















