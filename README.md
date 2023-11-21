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















