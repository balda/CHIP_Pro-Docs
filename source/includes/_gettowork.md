# Get Working With C.H.I.P. Pro

## Power In, Power Out

C.H.I.P. Pro can be powered in a few ways, all managed by the AXP209 power management circuit. For simple applications on the test desk, power can be provided over the micro USB connector from a USB power supply or powered USB hub. But C.H.I.P. is for building, and depending on the nature of your product, there are different power options to make it easier to make with C.H.I.P. Pro.

* **CHGIN** - connect 4.8 to 6 volts of power to this pin (and GND) to provide power for C.H.I.P. Pro. If you have a Lithium Polymer (LiPo) battery connected to BAT, then power provided to CHGIN will also charge the battery. 
* **BAT** - connect a 3.7 volts Lithium Polymer (LiPo) battery to this pin (and GND) to provide power to C.H.I.P. Pro and receive charge from power inputs.
* **VBUS** - connect 5 volts to this pin (and GND to pin 53) to provide power to C.H.I.P.. Power connected to VBUS will also charge a battery, just at a slower rate than from CHGIN

C.H.I.P. Pro has a three options for providing power to peripherals and sensors.

* **VCC-3V3** - provides 3.3 V for sensors.
* **IPSOUT** - the Intelligent Power Select provides up to 2.5 amps at up to 5 volts, depending on power provided at CHGIN or VBUS. If a 3.7V LiPo battery is the only source of power, IPSOUT will provide a bit less than 3.7 volts. In general, the voltage at IPSOUT is a bit less than voltage in, with a max voltage of 5 volts.
* **PWRON** - connect to ground to turn C.H.I.P. Pro on and boot the operating system.

If you need to provide power to a USB device connected to USB1, connect IPSOUT to an appropriate switching regulator to the USB connector pad on your circuit board.

TKTK - images showing power connections?

## Get an Operating System

Like it's larger brother C.H.I.P., C.H.I.P. Pro's GR8 SiP can run mainline Linux. This provides security, flexibility, robust tools, and open-source options for getting your product working. In the interest of power consumption and storage space, we have several options to best fit your production.

### Gadget OS

---GADGET--- TKTK

### Debian
If you need to, you can run a standard Debian distribution, complete with all the package managers and conveniences you know and love. While this is great for development, it may not be optimal to deliver your product with a full debian installation. 

#### Things you will need

 * C.H.I.P. Pro
 * Standard-USB to micro-USB connector
 * An appendage to hold down the FEL button
 * Separate computer with [Chrome](https://www.google.com/chrome/browser/desktop/index.html) or [Chromium](https://www.chromium.org/getting-involved/download-chromium) browser

#### Flash

Visit our OS flash site at [flash.getchip.com](http://flash.getchip.com) in Chrome or Chromium browser. Hold down the FEL button on C.H.I.P. Pro and follow all the instructions in the browser. If you haven't already, you'll be asked to install the CHIP Flasher Plug-in for Chrome.

### Use It 

Now that you have power and an operating system, you can connect to your C.H.I.P. Pro to test software and hardware, customize it, or load new software. There are two very important connections for this: serial and network. 

## Serial Connection

The most basic connection to C.H.I.P. Pro is a serial connection, controlled through a host computer's terminal program.

### UART

#### Things you will need

* USB-UART cable ([for example](https://www.amazon.com/Armorview-PL2303HX-RS232-Module-Converter/dp/B008AGDTA4))
* Drivers
* Soldering gun
* Solder
* Pin headers
* Computer with monitor (for example, a [C.H.I.P.](http://www.getchip.com/)!)
* Terminal program for Windows such as [cygwin](https://cygwin.com/) or [PuTTY](http://www.chipkin.com/using-putty-for-serial-com-connections-hyperterminal-replacement/) (OS X and Linux have terminals built-in)

A UART to USB serial connection between C.H.I.P. Pro and your computer offers the most comprehensive look at what's happening in C.H.I.P. Pro as it boots, since you can get all message output from the moment it starts booting. You'll need a USB to UART cable and the appropriate drivers for your computer's OS. 

For example, [this](https://www.amazon.com/Armorview-PL2303HX-RS232-Module-Converter/dp/B008AGDTA4) cable uses the Prolific hardware, with drivers [available on their site](http://www.prolific.com.tw/US/ShowProduct.aspx?pcid=41&showlevel=0041-0041). Another popular chipset for these cables is FTDI.

Connect the cable to your computer and the UART pins on C.H.I.P.-Pro. You'll need to solder some headers onto C.H.I.P.-Pro for a reliable connection to the loose wires on the cable. The black cable goes to ground, green is usually RX, and white is usually TX, but there's no guarantee. 

From your computer's terminal, use the command

``` 
screen /dev/tty.usbserial 115200 #OS X
screen /dev/tty.USB0 115200      #Ubuntu
```

Another popular program besides screen is `cu`. 

For Windows read [our guide](http://docs.getchip.com/chip.html#using-putty) on connecting with Putty or cygwin.

### USB Gadget Serial

#### Things you will need

* USB micro-USB A cable ([for example](http://www.cablewholesale.com/products/usb-firewire/usb-2.0-cables/product-10u2-03101bk.php))
* Computer with monitor (for example, a [C.H.I.P.](http://www.getchip.com/)!)
* Terminal program for Windows such as [cygwin](https://cygwin.com/) or [PuTTY](http://www.chipkin.com/using-putty-for-serial-com-connections-hyperterminal-replacement/) (OS X and Linux have terminals built-in)

If your OS is configured for gadget serial, this is usually the easiest way to get inside C.H.I.P. Pro's software is using USB Gadget serial. While you won't be able to get boot messages, since the serial emulation won't be ready, all you need is a USB micro to USB A cable to connect C.H.I.P. Pro to your computer. From your computer's terminal:

```
screen /dev/tty.usbmodem1440 115200 #OS X
screen /dev/tty.ACM0 115200         #Ubuntu
```

Note that for OS X, you either need to list out all the tty devices with `ls /dev/tty.usbm*` to find the actual ID, or use the tab key to autocomplete, like `screen /dev/tty.usbm <tab>`.

For Windows read [our guide](http://docs.getchip.com/chip.html#using-putty) on connecting with Putty or cygwin.

## Log In
Once you have connected via serial, you'll be prompted for a username and password. The defaults are `chip` and `chip`. Change your password with `pwd`.

## Network

Once you have connected to C.H.I.P. Pro with a serial connection, you can set it up for network access. How this happens depends on the OS you have loaded onto C.H.I.P. Pro. Most likely you'll be able to make basic connections to a WiFi network using either `connman` or `nmcli` in the command line.

### Connman

The basic commands to connect are done in a connman terminal. You can learn more about connman [here](https://wiki.archlinux.org/index.php/Connman)

```
sudo connmanctl # enter the connman terminal

> enable wifi # turn on wifi
> scan wifi # find networks
> agent on # let connman prompt for a password when needed
> services # list all the visible networks so you can get the wifi_ id string
> connect wifi_7cc70905cd77_4e5443_managed_psk #connman will then prompt for password
> quit # get back to linux terminal
```

If your network doesn't have a password

### nmcli

You may find `nmcli` is the gateway to your network. There's a lot of information about nmcli on the [archlinux site](https://wiki.archlinux.org/index.php/NetworkManager). If nmcli is what you need, here's the commands you can use to connect to a network using your serial connection in the terminal:

```
sudo nmcli d wifi # list visible wifi networks
sudo nmcli d wifi connect "Network SSID Name" password "Your Password" ifname wlan0 # if network is hidden add this to end: hidden yes
```

### ping!

It's always reassuring to check that you have a connection with ping:

```
ping 8.8.8.8 #google dns server
```

## Access I/O via sysfs	

### GPIO Input

These lines of code will let us read values on pin CSIDO, which corresponds to pin 132 in the linux sysfs (CSID0-CSID7 have numbers 132-139) First, we tell the system we want to listen to this pin:

```shell
  sudo sh -c 'echo 132 > /sys/class/gpio/export'
```

View the mode of the pin. This should return “in”:

```shell
  cat /sys/class/gpio/gpio132/direction
```

Connect a jumper wire or switch between Pin CSID0 and GND. Now use this line of code to read the value:

```shell
  cat /sys/class/gpio/gpio132/value
```

### GPIO Output

You could also change the mode of a pin from “in” to “out”

```shell
  sudo sh -c 'echo out > /sys/class/gpio/gpio132/direction'
```

Now that it's in output mode, you can write a value to the pin:

```shell
  sudo sh -c 'echo 1 > /sys/class/gpio/gpio132/value'
```

If you attach an LED to the pin and ground, the LED will illuminate according to your control messages.


### GPIO Done

When you are done experimenting, you can tell the system to stop listening to the gpio pin:

```shell
  sudo sh -c 'echo 132 > /sys/class/gpio/unexport'
```

### Finding GPIO Pin Names
You can calculate the sysfs pin number using the [Allwinner R8 Datasheet](https://github.com/NextThingCo/CHIP-Hardware/blob/master/CHIP%5Bv1_0%5D/CHIPv1_0-BOM-Datasheets/Allwinner%20R8%20Datasheet%20V1.2.pdf), starting on page 18. 

The letter index is a multiple of 32 (where A=0), and the number is an offset. For example PE4 is `CSID_D0` so

```
E=4
(32*4)+4 = 132
```

Therefore, listening to CSID0 in sysfs would begin with

```
sudo sh -c 'echo 132 > /sys/class/gpio/export'
```

# Open Source
The C.H.I.P. Pro is open source hardware. Get all the details in our [github repo](https://github.com/NextThingCo/C.H.I.P._Pro-Hardware).