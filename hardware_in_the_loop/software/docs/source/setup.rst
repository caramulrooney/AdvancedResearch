Setup
=====

DISCLAIMER: This process requires root permissions to edit some files.

Prerequisites
^^^^^^^^^^^^^
* A linux system. Due to the hardware interfaces that this project relies on, I STRONGLY recommend against using a virtual machine; this project will not work out of the box on a VM.
* A python environment on your computer. At the very least, you _should_ be able to use the version of python that came installed with your operating system, but I recommend setting up `pyenv <https://realpython.com/intro-to-pyenv/>`_ with virtual environments to isolate this project's dependencies.

Installation
^^^^^^^^^^^^

1. If you haven't yet, clone this repository onto your computer::

    $ git clone https://github.com/olin-electric-motorsports/AdvancedResearch.git

2. To perform software installation and setup, navigate to the software directory::
    
    $ cd AdvancedResearch/hardware_in_the_loop/software

3. (Optional) If you want to setup a virtual environment for this project (I recommend it), now is the time. If you don't know how to do this, read `here <https://realpython.com/intro-to-pyenv/>`_

4. Use pip to install the project and its dependencies on your computer. If you usually use ``pip3`` to invoke ``pip``, use that instead; as long as the actual version of ``pip`` is >3.6.0, you should be fine.::

    $ pip install -e .

5. Now that the software is installed, it's time to configure hardware. For now, the only hardware we can connect to is an arduino. Go ahead and plug that in now. If you don't have an arduino, thats fine; you just won't be able to run all unit tests.

6. Now that your arduino is plugged in, verify that your computer recognizes it with::

    `$ lsusb`
    
You should see a your arduino listed as an option. If you don't **do not** proceed to step 6; try unplugging it and plugging it in again.
    
7. Navigate to our ``scripts`` directory and run our hardware setup script::

    $ cd scripts && sudo python hardware_setup.py

This script creates a udev rule which generates a permanent symbolic link to your arduino at ``/dev/arduino``, so we never need to guess where to find it. The software defaults to these symbolic links if they are not specified in ``config.ini``.

8. Restart your computer.::

    $ sudo shutdown -r now

It is generally recommended to restart to reload udev rules. If you're in a rush, you can try::
    
    $ sudo udevadm control --reload-rules

but I generally recommend restarting just to be sure.

Common issues
^^^^^^^^^^^^^

* **Wrong/mismatched python versions**
    
    If you're having trouble using pip or python (especially when running with ``sudo``), make sure you are using the right python version with ``$ which python`` or ``$ which python3``. When I was setting this up, I noticed I was using the expected python interpreter when I called ``python3`` or ``pip3``, but as soon as I ran ``sudo python3`` or ``sudo pip3``, the python version was different. If this is confusing and you don't know how to resolve it, please just follow the virtual environment tutorial I linked above to setup python >=3.7 on your machine.

* **Missing hardware permissions**

    If the ``hardware_setup.py`` script is returning a ``no langid`` error or similar, it is probably because your user doesn't have permission to get certain information from the USB device. Try running this command with ``sudo`` (and, as noted above, make sure you are using the expected python version).