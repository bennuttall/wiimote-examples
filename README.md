# wiimote-examples

How to use a Wiimote with a Raspberry Pi

[incomplete guide]

## Install cwiid

cwiid is the Python library used to communicate with the Wiimote. Install with:

```bash
sudo apt install libcwiid1 -y
sudo pip3 install cwiid
```

## Example code

```python
import cwiid

wii = None
while not wii:
    try:
        wii = cwiid.Wiimote()
    except:
        print("Hold down Wiimote buttons")

wii.rpt_mode = cwiid.RPT_BTN

while True:
    buttons = wii.state['buttons']
    if buttons & cwiid.BTN_UP:
        print("up")
    elif buttons & cwiid.BTN_DOWN:
        print("down")
    elif buttons & cwiid.BTN_LEFT:
        print("left")
    elif buttons & cwiid.BTN_RIGHT:
        print("right")
    elif buttons & cwiid.BTN_A:
        print("A")
    elif buttons & cwiid.BTN_B:
        print("B")
```

The Wiimote's A & B buttons need to be held down to connect:

```python
wii = None
while not wii:
    try:
        wii = cwiid.Wiimote()
    except:
        print("Hold down Wiimote buttons")
```

The mode must be set:

```python
wii.rpt_mode = cwiid.RPT_BTN
```

`wii.state['buttons']` is a number which tells you which buttons are pressed. Each button is assigned a power of two (1, 2, 4, 8...) and so the total number in `wii.state['buttons']` is the sum of all these numbers, so you can work out which combination is pressed:

[table]
