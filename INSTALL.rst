Installation
=================

This document describes how to install all dependencies needed to use Alex.
The Alex project is developed in Python and tested with version 2.7.
It may be necessary to have exactly this version of Python for the project
to work correctly.

Local installation of Python 2.7 and dependencies
-------------------------------------------------

If you do not have the root access to the machine then you then you can use https://github.com/akheron/multipy to install
the 2.7 version of Python and consequently to install all Python dependencies locally.

You can use the following script

.. code-block:: bash

  $ multipy install 2.7

to download, compile, and install python 2.7 into ``~/multipy`` directory.

To enable this local version, you have to call from your shell command line

.. code-block:: bash

  $ source ~/multipy/pythons/2.7/bin/activate

You can also add the previous line into ``.bashrc`` to activate your local
version of Python every time you start a bash console.

Ubuntu 12.04
------------

Ask the root on the computer to run:

.. code-block:: bash

    $ sudo apt-get install gfortran libatlas-base-dev portaudio19-dev \
        flac speex sox mplayer libsqlite3-dev python-wxgtk2.8

To get latest versions of the following python packages, I recommend to run these commands:

.. code-block:: bash

    $ sudo pip install --upgrade numpy     # We require 1.7.1
    $ sudo pip install --upgrade scipy
    $ sudo pip install --upgrade scikit-learn
    $ sudo pip install --upgrade wxpython
    $ sudo pip install --upgrade matplotlib

    $ sudo pip install --upgrade pysqlite
    $ sudo pip install --upgrade sqlalchemy
    $ sudo pip install --upgrade pyga
    $ sudo pip install --upgrade python-Levenshtein
    $ sudo pip install --upgrade boto
    $ sudo pip install --upgrade pysox
    $ sudo pip install --upgrade jinja2

    $ sudo easy_install wget
    $ sudo easy_install pymad
    $ sudo easy_install ipdb


Source compiled packages
------------------------

pyAudio
~~~~~~~
Get a special version of pyAudio from https://github.com/bastibe/PyAudio (bastibe-PyAudio-2a08fa7)
This version supports non-blocking audio.

.. code-block:: bash

    $ git clone https://github.com/bastibe/PyAudio 
    $ cd PyAudio
    $ python ./setup.py install

flite
~~~~~
- get the lates flite
- build flite

.. code-block:: bash

    $ bunzip2 flite-1.4-release.tar.bz2
    $ tar -xvf flite-1.4-release.tar
    $ cd flite-1.4-release
    $ ./configure
    $ make

- put ``flite-1.4-release/bin/flite`` into you search path. E.g. link the flite program to your bin directory

HTK
~~~~
- get the latest HTK (3.4.1 tested) from http://htk.eng.cam.ac.uk/download.shtml
- build and install the HTK

SRILM
~~~~~
- get the latest SRILM (1.6 tested) from http://www.speech.sri.com/projects/srilm/
- build and install the SRILM

pjsip
~~~~~
Get the supported pjsip 2.1 from our fork at GitHub.
To install pjsip, follow the next instructions:

.. code-block:: bash

    $ git clone git@github.com:UFAL-DSG/pjsip.git
    $ cd pjsip
    $ ./configure CXXFLAGS=-fPIC CFLAGS=-fPIC LDFLAGS=-fPIC CPPFLAGS=-fPIC
    $ make dep
    $ make
    $ make install

then 

.. code-block:: bash

    $ cd pjsip-apps/src/python/
    $ python setup-pjsuaxt.py install

this will install the extended pjsuaxt library.

Julius
~~~~~~
Get the supported Open Julius ASR decoder (4.2.3 tested) from our fork at GitHub.
To install openjulius, follow the following instructions:

.. code-block:: bash

    $ git clone git@github.com:UFAL-DSG/openjulius.git
    $ cd openjulius
    $ ./configure
    $ make
    $ make install

Optimised ATLAS and LAPACK libraries
------------------------------------

If you need optimised ATLAS and LAPACK libraries then you have to compile them on your own.
Then modify config for numpy. Optimised ATLAS and LAPACK can compute matrix multiplication on all CPU cores available.

To build your own optimised ATLAS and LAPACK libraries:

- get latest LAPACK
- get latest ATLAS
- compile lapack
- tell atlas where is your compiled LAPACK
- compile ATLAS
