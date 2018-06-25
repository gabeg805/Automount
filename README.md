# AUTOMNT

## Introduction

This program is used to automatically mount a removable device that is inserted
into your computer.


## How it works

When a USB device is plugged into your computer, a file is created in the
*/dev/block* directory. This file is named something of the form *8:17* and
points to the actual device name, e.g. *sdb1*.

Systemd services are used to monitor the */dev/block* directory, and then
execute a service once a change is made to that directory. The service will call
the *automnt* script, which will iterate over all files in that directory, use
*stat* to determine the most recently created file(s), and mount them.

There are restrictions as to what can be mounted, however. To name a few:
- The file must have been created within 10 seconds of the script being called.
- The file may not have the name *sda#*
- The file must be a partition, e.g. *sdX#*. This means *sdX* will not be
  mounted.
- The file must not point to a device that is already mounted.

## Requirements

- systemctl
- udisks

## Install

```
./automnt --install
```

The program should be up and running, waiting for a USB to be plugged in.

You can check this by running:
```
systemctl --user status automnt.path
```

## Uninstall

```
./automnt --uninstall
```
