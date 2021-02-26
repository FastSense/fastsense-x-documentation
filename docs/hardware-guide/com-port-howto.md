# UART how-to

## How to get access to the serial ports?

In order to start communicating with serial ports, you need to add the user into the `tty` and `dialout` groups.

```
groups username
sudo usermod -a -G tty username
sudo usermod -a -G dialout username
```

## How to change the speed?

There is *stty* util in lubuntu, which allows you to interact with serials.

Find out port parameters:

```
stty -a -F /dev/ttyS*
```

Set default port speed:

```
stty -F /dev/ttyS* 115200
```

Supported speeds: 1200, 2400, 4800, 9600, 14400, 19200, 38400, 57600, 115200, 921600.