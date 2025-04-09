Some Xilinx Platform Cables (old/clones) are not supported on AMD Vivado, using those files fxload will load appropriate FW as soon as adapter is connected to USB

Tested on Xilinx Platform Cable USB Clone [CY7C68013A + XC2C256 + 24C02N]

install util
```bash
sudo apt install fxload
```

copy udev rules
```bash
sudo cp xusbdfwu.rules /etc/udev/rules.d/
```

make sure you have /etc/udev/rules.d/52-xilinx-pcusb.rules
```bash
ATTR{idVendor}=="03fd", ATTR{idProduct}=="0008", MODE="666"
ATTR{idVendor}=="03fd", ATTR{idProduct}=="0007", MODE="666"
ATTR{idVendor}=="03fd", ATTR{idProduct}=="0009", MODE="666"
ATTR{idVendor}=="03fd", ATTR{idProduct}=="000d", MODE="666"
ATTR{idVendor}=="03fd", ATTR{idProduct}=="000f", MODE="666"
ATTR{idVendor}=="03fd", ATTR{idProduct}=="0013", MODE="666"
ATTR{idVendor}=="03fd", ATTR{idProduct}=="0015", MODE="666"
```

copy .hex files to /etc/xilinx-xusb/
```bash
sudo mkdir -p /etc/xilinx-xusb/
sudo cp *.hex /etc/xilinx-xusb/
```

reload udev
```bash
sudo udevadm control --reload-rules
sudo udevadm trigger
```

Finally, reconnect Xilinx Adapter
