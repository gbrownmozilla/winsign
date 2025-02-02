=======
winsign
=======

.. image:: https://img.shields.io/pypi/v/winsign.svg
        :target: https://pypi.python.org/pypi/winsign

.. image:: https://readthedocs.org/projects/winsign/badge/?version=latest
        :target: https://winsign.readthedocs.io/en/latest/?badge=latest
        :alt: Documentation Status

`winsign` is a python module for signing and manipulating `Authenticode
<https://en.wikipedia.org/wiki/Code_signing#Implementations>`_ signatures in PE and MSI files.

* Works on Python 3.7 and up.
* Free software: MPL2

Requirements
============
Most dependencies are specified in requirements/base.txt, however, currently
you also need `osslsigncode` installed to perform signing. This utility can be
fetched from your distribution's package repository, or from e.g.
https://github.com/theuni/osslsigncode

Signing MSIX/APPX files currently requires Mozilla's fork of `msix-packaging
<https://github.com/mozilla/msix-packaging/tree/johnmcpms/signing>`_.

Installation
============
`pip install winsign`

CLI Usage
=========
::

   usage: winsign [-h] --certs CERTS --key PRIV_KEY [-n COMMENT] [-i URL] -d
                  {sha1,sha256} [-t {old,rfc3161}] [-v] [-q]
                  infile [outfile]

   positional arguments:
     infile            unsigned file to sign
     outfile           where to write output to. defaults to infile

   optional arguments:
     -h, --help        show this help message and exit
     --certs CERTS     certificates to include in the signature
     --key PRIV_KEY    private key used to sign
     -n COMMENT        comment to include in signature
     -i URL            url to include in signature
     -d {sha1,sha256}  digest to use for signing. must be one of sha1 or sha256
     -t {old,rfc3161}
     -v, --verbose
     -q, --quiet

Future plans
============
* Stop using osslsigncode for PE signatures
* Refactor code so that osslsigncode functionality is in its own module
* Add python support for MSI, then we can drop dependency on osslsigncode

Development
===========
Highly recommended to create a virtualenv, then run:
 * *python setup.py develop*
 * make your changes to the source files
 * run local tests: *tox*

upon successful r+ and merging to *master* branch, you need to release a new version on PyPi.
 * edit setup.py to adjust the version
 * generate .whl file locally: *python setup.py bdist_wheel*
 * file will exist in: *./dist/winsign-{version}-py3-none-any.whl*
 * (assuming you have pypi access to upload)
 * upload to pypi: *twine upload --verbose dist/winsign-{version}-py3-none-any.whl*

Credits
=======

* Chris AtLee
* Ben Hearsum <bhearsum@mozilla.com>
* Joel Maher <jmaher@mozilla.com>
