Python language bindings for ev3dev
===================================

.. image:: https://travis-ci.org/rhempel/ev3dev-lang-python.svg?branch=master
    :target: https://travis-ci.org/rhempel/ev3dev-lang-python
.. image:: https://readthedocs.org/projects/python-ev3dev/badge/?version=latest
    :target: http://python-ev3dev.readthedocs.org/en/latest/?badge=latest
    :alt: Documentation Status

A Python3 library implementing an interface for ev3dev_ devices,
letting you control motors, sensors, hardware buttons, LCD
displays and more from Python code.

If you haven't written code in Python before, you'll need to learn the language
before you can use this library.

Getting Started
---------------

This library runs on ev3dev_. Before continuing, make sure that you have set up
your EV3 or other ev3dev device as explained in the `ev3dev Getting Started guide`_.
Make sure that you have a kernel version that includes ``-10-ev3dev`` or higher (a
larger number). You can check the kernel version by selecting "About" in Brickman
and scrolling down to the "kernel version". If you don't have a compatible version,
`upgrade the kernel before continuing`_.

Once you have booted ev3dev and connected to your EV3 (or Raspberry Pi / BeagleBone)
via SSH, you will need to install the latest version of this library.

To do so, run the following commands, which could take ten minutes or longer
(you may be prompted to type the password; the default is ``maker``):

.. code-block:: bash

   sudo apt-get update
   sudo apt-get install python3-ev3dev

Now that you have the latest version installed, you should be ready to start
using ev3dev with Python. If you want to go through some basic usage examples,
check out the `Usage Examples`_ section to try out motors, sensors and LEDs.
Then look at `Writing Python Programs for Ev3dev`_ to see how you can save
your Python code to a file.

Make sure that you look at the `User Resources`_ section as well for links
to documentation and larger examples.

Usage Examples
------------

To run these minimal examples, run the Python3 interpreter from
the terminal using the ``python3`` command: 

.. code-block::

  $ python3
  Python 3.4.2 (default, Oct  8 2014, 14:47:30) 
  [GCC 4.9.1] on linux
  Type "help", "copyright", "credits" or "license" for more information.
  >>>

The ``>>>`` characters are the default prompt for Python. In the examples
below, we have removed these characters so it's easier to cut and 
paste the code into your session.

Required: Import the library
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

  import ev3dev.ev3 as ev3

Controlling the LEDs with a touch sensor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This code will turn the left LED red whenever the touch sensor is pressed, and
back to green when it's released. Plug a touch sensor into any sensor port and
then paste in this code - you'll need to hit ``Enter`` after pasting to complete
the loop and start the program.  Hit ``Ctrl-C`` to exit the loop.

.. code-block:: python

  ts = ev3.TouchSensor()
  while True:
      ev3.Leds.set_color(ev3.Leds.LEFT, (ev3.Leds.GREEN, ev3.Leds.RED)[ts.value()])

Running a motor
~~~~~~~~~~~~~~~

Now plug a motor into the ``A`` port and paste this code into the Python prompt.
This little program will run the motor at 500 ticks per second (around 0.4
rotations per second) for three seconds.

.. code-block:: python

  m = ev3.LargeMotor('outA')
  m.run_timed(time_sp=3000, speed_sp=500)

Using text-to-speech
~~~~~~~~~~~~~~~~~~~~

If you want to make your robot speak, you can use the `Sound.speak` method:

.. code-block:: python

  ev3.Sound.speak('Welcome to the E V 3 dev project!').wait()

**To quit the Python REPL, just type** ``exit()`` **or press** ``Ctrl-D`` **.**

Make sure to check out the `User Resources`_ section for more detailed
information on these features and many others.

Writing Python Programs for Ev3dev
----------------------------------

Every Python program should have a few basic parts. Use this template
to get started:

.. code-block:: python
   
   #!/usr/bin/env python3
   from ev3dev.ev3 import *

   # TODO: Add code here

The first two lines should be included in every Python program you write
for ev3dev. The first allows you to run this program from Brickman, while the
second imports this library.

When saving Python files, it is best to use the ``.py`` extension, e.g. ``my-file.py``.

User Resources
--------------

Library Documentation
    **Class documentation for this library can be found on** `our Read the Docs page`_ **.**
    You can always go there to get information on how you can use this
    library's functionality.

ev3dev.org
    `ev3dev.org`_ is a great resource for finding guides and tutoials on
    using ev3dev.

Support
    If you are having trouble using this library, please open an issue
    at `our Issues tracker`_ so that we can help you. When opening an
    issue, make sure to include as much information as possible about
    what you are trying to do and what you have tried. The issue template
    is in place to guide you through this process.

Demo Robot
    Laurens Valk of robot-square_ has been kind enough to allow us to
    reference his excellent `EXPLOR3R`_ robot. Consider building the
    `EXPLOR3R`_ and running the demo programs referenced below to get
    familiar with what Python programs using this binding look like.

Demo Code
    There are `demo programs`_ that you can run to get acquainted with
    this language binding. The programs are designed to work with the
    `EXPLOR3R`_ robot.

Developer Resources
-------------------

Python Package Index
    The Python language has a `package repository`_ where you can find
    libraries that others have written, including the `latest version of
    this package`_.

The ev3dev Binding Specification
    Like all of the language bindings for ev3dev_ supported hardware, the
    Python binding follows the minimal API that must be provided per
    `this document`_.

The ev3dev-lang Project on GitHub
    The `source repository for the generic API`_ and the scripts to automatically
    generate the binding. Only developers of the ev3dev-lang-python_ binding 
    would normally need to access this information.

Python2.x and Python3.x Compatibility
-------------------------------------

The ev3dev_ distribution comes with both python2_ and python3_ installed
but this library is compatible only with Python3.

Note that currently, the Python3 binding for ev3dev_ is not installed
by default - this will be addressed in the next package we
release.

Until then, you must follow the instructions at the top of this README to make
sure that you have installed the newest version of the Python 3-based library.

.. _ev3dev: http://ev3dev.org
.. _ev3dev.org: ev3dev_
.. _Getting Started: ev3dev-getting-started_
.. _ev3dev Getting Started guide: ev3dev-getting-started_
.. _ev3dev-getting-started: http://www.ev3dev.org/docs/getting-started/
.. _upgrade the kernel before continuing: http://www.ev3dev.org/docs/tutorials/upgrading-ev3dev/
.. _detailed instructions for USB connections: ev3dev-usb-internet_ 
.. _ev3dev-usb-internet: http://www.ev3dev.org/docs/tutorials/connecting-to-the-internet-via-usb/
.. _our Read the Docs page: http://python-ev3dev.readthedocs.org/en/latest/
.. _source repository for the generic API: ev3dev-lang_
.. _ev3dev-lang: https://github.com/ev3dev/ev3dev-lang
.. _ev3dev-lang-python: https://github.com/rhempel/ev3dev-lang-python
.. _our Issues tracker: https://github.com/rhempel/ev3dev-lang-python/issues
.. _this document: wrapper-specification_
.. _wrapper-specification: https://github.com/ev3dev/ev3dev-lang/blob/develop/wrapper-specification.md
.. _EXPLOR3R: demo-robot_
.. _demo-robot: http://robotsquare.com/2015/10/06/explor3r-building-instructions/
.. _demo programs: demo-code_
.. _demo-code: https://github.com/rhempel/ev3dev-lang-python/tree/master/demo
.. _robot-square: http://robotsquare.com/
.. _Python 2.x: python2_
.. _python2: https://docs.python.org/2/
.. _Python 3.x: python3_
.. _python3: https://docs.python.org/3/
.. _package repository: pypi_
.. _pypi: https://pypi.python.org/pypi
.. _latest version of this package: pypi-python-ev3dev_
.. _pypi-python-ev3dev: https://pypi.python.org/pypi/python-ev3dev
