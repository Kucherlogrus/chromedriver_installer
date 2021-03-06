ChromeDriver Installer for Python
=================================

This is a fork `ChromeDriver Installer for Python <https://github.com/Kucherlogrus/chromedriver_installer.git>`__ repository

Installs `ChromeDriver executable <https://sites.google.com/a/chromium.org/chromedriver/>`__
with **pip** or **setup.py**.

Usage
-----

Manual Installation
^^^^^^^^^^^^^^^^^^^

Clone the repository:

.. code-block:: bash

    (e)$ git clone https://github.com/Kucherlogrus/chromedriver_installer.git

Install the most recent **ChromeDriver** version without verifying checksum.

.. code-block:: bash

    (e)$ python setup.py install

Install specific **ChromeDriver** version without verifying checksum.

.. code-block:: bash

    (e)$ python setup.py install --chromedriver-version=2.10

Install specific **ChromeDriver** version and verify checksum.
Note that you can pass multiple coma-separated checksums to the
``--chromedriver-checksums`` option. This is useful if you plan to install
**ChromeDriver** on various platforms because there is separate version with
different checksum for each platform. You can get the checksums for specific
version/platform combinations at the
`chromedriver download URL <http://chromedriver.storage.googleapis.com/index.html>`__.

.. code-block:: bash

    (e)$ python setup.py install \
        --chromedriver-version=2.10 \
        --chromedriver-checksums=4fecc99b066cb1a346035bf022607104,058cd8b7b4b9688507701b5e648fd821

After install, there should be the ``chromedriver`` executable
available in your path:

.. code-block:: bash

    (e)$ which chromedriver
    /home/andypipkin/e/bin/chromedriver
    (e)$ chromedriver --version
    ChromeDriver 2.10.267518
    (e)$ chromedriver
    Starting ChromeDriver (v2.10.267518) on port 9515
    Only local connections are allowed.


Installation With PIP
^^^^^^^^^^^^^^^^^^^^^

The same as before except you need to pass the install options wrapped in pip's
``--install-option=""`` option.

.. code-block:: bash

    (e)$ pip install chromedriver_installer \
        --install-option="--chromedriver-version=2.10" \
        --install-option="--chromedriver-checksums=4fecc99b066cb1a346035bf022607104,058cd8b7b4b9688507701b5e648fd821"

Installation With easy_install
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

I can't seem to find a way to make **easy_install** pass *user options* to
**setup.py** so you only can install the most recent
**ChromeDriver** version with **easy_install**.

How it Works
------------

The **build_scripts** command of the **setup.py** script invoked by
``python setup.py install`` downloads, the **ChromeDriver** zip archive version
specified in the ``--chromedriver-version`` option from
http://chromedriver.storage.googleapis.com/index.html
to the **temp** directory of the operating system.
If the ``--chromedriver-checksums`` option is set, the archive is validated
against the supplied checksums
(you can get the checksums at the aforementioned URL).
If the validation failed, the installation exits with an error.
If the validation was successful or if the ``--chromedriver-checksums`` option
is not set, the archive will be unzipped to the *build directory* and installed
as an executable to the *bin directory*.

If the ``--chromedriver-version`` option is ommited, it installs the most recent
chromedriver version without checksum validation.


Testing
-------

You need `tox <https://testrun.org/tox/latest/>`__ to run the tests.

.. code-block:: bash

    (e)$ git clone https://github.com/peterhudec/chromedriver_installer.git
    (e)$ pip install -r requirements.txt
    (e)$ tox
