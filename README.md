===========
What is it?
===========

This program is used to automount a USB device. When a USB device is plugged in,
originally, it is not mounted, however, a file is created in '/dev/block/'. This
program watches the '/dev/block/' directory and waits for a change. When the 
directory is modified (i.e. when something is added/removed or a file changes), this 
program automatically mounts the USB device that is plugged in at '/media/'.



=============
Documentation
=============

Requires:
    
    - udisks

The program "autousb" is responsible for mounting the USB device. The systemd file 
"detect-usb.path" watches the "/dev/block/" directory for any changes. When there is
a change, it starts the "detect-usb.service" service file which executes the 
"autousb" program.

Further documentation can be found in the program header.



============
Installation
============

Modify the systemd files so that they reflect your "autousb" path:
    
    $ <text editor> ./src/systemd/detect-usb.service

Find the line that says:
    
    ExecStart=/mnt/Linux/Share/scripts/programs/automount/autousb

And change it so that it looks like:
    
    ExecStart=/PATH/TO/PROGRAM/autousb

Now enable the systemd files so that they watch the "/dev/block/" directory:
    
    # cp ./src/systemd/detect-usb.* /usr/lib/systemd/system/
    # systemctl enable detect-usb.path
    # systemctl enable detect-usb.service

On the next reboot, these service files will be activated and wait for a USB to be
mounted!

Lastly, update your PATH environment variable in your shell rc file with:
    
    $ export PATH="${PATH}":"/PATH/TO/PROGRAM/autousb"

Now the program is ready for use!



========
Contacts
========

If you have any problems, feel free to email me at 'gabeg@bu.edu'.



==================
Potential Problems
==================

- If the USB device does not get mounted.
    * There are three ways to diagnose this issue:
        
            # ls /media/
            # systemctl status detect-usb.path
            # systemctl status detect-usb.service
      
      If the first command does not show any results, then unfortunately, you'll have
      to see what is displayed in the last two commands and go from there. Sorry!



=====
To-Do
=====

- TBD
