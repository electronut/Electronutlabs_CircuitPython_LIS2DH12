Introduction
============

.. image:: https://readthedocs.org/projects/circuitpython-lis2dh12-library/badge/?version=latest
    :target: https://circuitpython-lis2dh12-library.readthedocs.io/en/latest/
    :alt: Documentation Status

.. image:: https://img.shields.io/discord/327254708534116352.svg
    :target: https://discord.gg/nBQh6qu
    :alt: Discord

.. image:: https://api.travis-ci.org/electronut/Electronutlabs_CircuitPython_LIS2DH12.svg?branch=master
    :target: https://travis-ci.org/electronut/Electronutlabs_CircuitPython_LIS2DH12/
    :alt: Build Status

Circuitpython library for LIS2DH12 3-axis low power accelerometer.


Dependencies
=============
This driver depends on:

* `Adafruit CircuitPython <https://github.com/adafruit/circuitpython>`_
* `Bus Device <https://github.com/adafruit/Adafruit_CircuitPython_BusDevice>`_

Please ensure all dependencies are available on the CircuitPython filesystem.
This is easily achieved by downloading
`the Adafruit library and driver bundle <https://github.com/adafruit/Adafruit_CircuitPython_Bundle>`_.

Usage Example
=============

.. code-block:: python

    import time
    import board
    import busio
    import electronutlabs_lis2dh12

    i2c = busio.I2C(board.SCL, board.SDA)
    lis2dh12 = electronutlabs_lis2dh12.LIS2DH12_I2C(i2c, address=0x19)

    lis2dh12.range = electronutlabs_lis2dh12.RANGE_2_G

    while True:
        # Read accelerometer values (in m / s ^ 2).  Returns a 3-tuple of x, y,
        # z axis values.  Divide them by 9.806 to convert to Gs.
        x, y, z = [value / electronutlabs_lis2dh12.STANDARD_GRAVITY for value in lis2dh12.acceleration]
        print("x = %0.3f G, y = %0.3f G, z = %0.3f G" % (x, y, z))
        # Small delay to keep things responsive but give time for interrupt processing.
        time.sleep(0.5)

Contributing
============

Contributions are welcome! Please read our `Code of Conduct
<https://github.com/electronut/Electronutlabs_CircuitPython_LIS2DH12/blob/master/CODE_OF_CONDUCT.md>`_
before contributing to help this project stay welcoming.

Building locally
================

Zip release files
-----------------

To build this library locally you'll need to install the
`circuitpython-build-tools <https://github.com/adafruit/circuitpython-build-tools>`_ package.

.. code-block:: shell

    python3 -m venv .env
    source .env/bin/activate
    pip install circuitpython-build-tools

Once installed, make sure you are in the virtual environment:

.. code-block:: shell

    source .env/bin/activate

Then run the build:

.. code-block:: shell

    circuitpython-build-bundles --filename_prefix electronutlabs-circuitpython-lis2dh12 --library_location .

Sphinx documentation
-----------------------

Sphinx is used to build the documentation based on rST files and comments in the code. First,
install dependencies (feel free to reuse the virtual environment from above):

.. code-block:: shell

    python3 -m venv .env
    source .env/bin/activate
    pip install Sphinx sphinx-rtd-theme

Now, once you have the virtual environment activated:

.. code-block:: shell

    cd docs
    sphinx-build -E -W -b html . _build/html

This will output the documentation to ``docs/_build/html``. Open the index.html in your browser to
view them. It will also (due to -W) error out on any warning like Travis will. This is a good way to
locally verify it will pass.
