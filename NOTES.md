# Up and Running

## Raspberry Pi image

- https://drive.google.com/file/d/1vr4nEXLEh4xByKAXik8KhK3o-XWgo2fQ/view
- Unzip and create disk image using a program like [Etcher](https://www.balena.io/etcher/)
- Once image is made, open `boot` partition of drive and make a file called:
  `wpa_supplicant.conf` and add the following. Code snippet to setup wifi for your first boot.
```
country=AU
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="your network name...keep the quotes"
    psk="wifi passwork...keep the quotes"
}
```

- Remove drive, put into Pi, and power on.
- User name: pi
- Password raspberry
- The image you flashed using Etcher only has libraries for Tensorflow. Now we need to install donkeycar: `pip install donkeyca[pi]`
- now run `donkey create car ~/mycar`



---

Looks like we can modify this file to insert messaging for control:

`~/env/lib/python3.5/site-packages/donkeycar/parts/actuator.py`

The controllers are initialized here: `line 103: manage.py` using the module above.

# Webcam

- Install `pygame` 
```
$ pip install pygame
$ sudo apt-get install libsdl-ttf2.0-0
```

- Modify `manage.py`

```
# minus (-) is existing code that should be commented out.
# plus  (+) is the new code you need to add

- from donkeycar.parts.camera import PiCamera
+ from donkeycar.parts.camera import Webcam as Cam
```

and

```
- cam = PiCamera(resolution...)
+ cam = Cam(resolution...)
```
