
# Fix Touchpad ChromeOs Brunch FrameWork

this problem is often found when the touchpad is detected in the command "cat /proc/bus/input/devices" but any movement on the touchpad doesn't work at all but clicks work, some have a blank screen when the touchpad is clicked
## Problem

- I suspect that some of the touchpads lose resolution on Chromeos, it's because Chromeos itself doesn't extend enough for their drivers.

- and I suspect also that chromeos doesn't link some touchpads to the correct drivers, touchpads don't work properly due to lack of information given by the OS to the touchpad itself
## Disclaimer
Not all touchpads support this way
## Fixing


Open terminal `Ctrl + Alt + T` then `shell` 

Then run this command

```bash
  sudo nano /etc/gesture/40-touchpad-cmt.conf
```
you should see an image like the one below, the code will be slightly different because I have edited mine

<p align="center">
   <img src="https://github.com/Irfan234-afif/FIX-TOUCHPAD-BRUNCH-CHROMEOS/blob/main/Images/Screenshot%202023-05-06%2022.19.34.png"
</p>

understand the code blocks!

We'll change the code in the first block, because that's where the core of the touchpad configuration.

```bash 
Section "InputClass"
    Identifier      "touchpad"
    MatchIsTouchpad "on"
    MatchDevicePath "/dev/input/event*"
    Driver          "cmt"
    Option          "AccelerationProfile" "-1"
    Option          "Scroll Buttons" "0"
    Option          "Scroll Axes" "1"

    # CMT devices potentially process keyboard events
    Option          "XkbModel" "pc"
    Option          "XkbLayout" "us"
EndSection
```

the code above is the default code, we will add the code in the options.

Add code this 

```bash
    Option          "Tap Minimum Pressure" "-15.0"
    Option          "Horizontal Resolution" "33"
    Option          "Vertical Resolution" "33"

    Option          "Two Finger Vertical Close Distance Thresh" "35.0"
    Option          "Fling Buffer Suppress Zero Length Scrolls" "0"
```

then the code will be like this

```bash
Section "InputClass"
    Identifier      "touchpad"
    MatchIsTouchpad "on"
    MatchDevicePath "/dev/input/event*"
    Driver          "cmt"
    Option          "AccelerationProfile" "-1"
    Option          "Scroll Buttons" "0"
    Option          "Scroll Axes" "1"

    Option          "Tap Minimum Pressure" "-15.0"
    Option          "Horizontal Resolution" "33"
    Option          "Vertical Resolution" "33"

    Option          "Two Finger Vertical Close Distance Thresh" "35.0"
    Option          "Fling Buffer Suppress Zero Length Scrolls" "0"

    # CMT devices potentially process keyboard events
    Option          "XkbModel" "pc"
    Option          "XkbLayout" "us"
EndSection
```
Actually the code that you have to add is the code in the second paragraph of the option

then ```Ctrl + X``` and ```Y```  last  ```enter```

reboot your CHROMEOS with type ```sudo reboot``` in terminal. 

Enjoy with your TouchPad
## Support

For support, email apipiirpan@gmail.com .

