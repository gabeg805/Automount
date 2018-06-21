# AUTOMNT

## What is it?

This program is used to automount a USB device.

When a USB device is plugged in, originally, a file is created in the
*/dev/block* directory. This program uses systemd files to watch that directory
for a change. When the directory is modified (e.g. when something is
added/removed or a file changes), this program automatically mounts the USB
device that is plugged in.

## Requirements

```    
- systemd: Detect devices plugged into/out-of the computer.
- udisks: Mount detected devices. 
```

## Installation

```
$ sudo ./automnt --install
```

The program should be up and running, waiting for a USB to be plugged in.

You can check this by running:
```
$ systemctl --user status automnt.path
```

## Uninstall

```
$ sudo ./automnt --uninstall
```
