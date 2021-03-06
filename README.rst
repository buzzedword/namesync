namesync |build-status| |python-versions|
==============================================

Sync DNS records stored in a flat file format to your DNS provider. Cloudflare support currently provided.

.. |build-status| image:: https://secure.travis-ci.org/dnerdy/namesync.svg?branch=master
    :alt: Build Status
    :target: http://travis-ci.org/dnerdy/namesync

.. |python-versions| image:: https://img.shields.io/badge/python-2.7_3.4-blue.svg
    :alt: Python Versions

Installation |pypi-version|
---------------------------

::

    $ pip install namesync

.. |pypi-version| image:: https://img.shields.io/pypi/v/namesync.svg
    :alt: PyPI Version
    :target: http://pypi.python.org/pypi/namesync

Quick Guide
-----------

Create a file with the name of your domain::
    
    $ touch example.com

Enter one record per line with the following format::
   
   <record-type> <name> <value> <ttl:optional>

For example::

    A       *       10.10.10.10         # You can even use comments
    A       .       10.10.10.10         # . references the domain itself, example.com
    A       test    10.10.10.11
    A       example 10.10.10.12 86400
    CNAME   mail    ghs.googlehosted.com
    MX      .       aspmx.l.google.com

MX records allow you to specify a priority::

   MX <name> <value> <priority:optional> <ttl:optional>

Like this::

    MX      .       alt1.aspmx.l.google.com 20
    MX      .       aspmx3.googlemail.com 30 86400

If the value contains spaces, quote it::

    TXT     .       "v=spf1 a include:amazonses.com include:_spf.google.com ~all"

Perform a dry run to see what will happen::

   $ namesync --dry-run example.com

If everything looks good, sync for real::

   $ namesync example.com

Usage
-----

::

    usage: namesync [-h] [-d DATA_DIR] [-z ZONE] [-t] records

    positional arguments:
      records

    optional arguments:
      -h, --help            show this help message and exit
      -d DATA_DIR, --data-dir DATA_DIR
      -z ZONE, --zone ZONE
      -t, --dry-run

