|Status|

Introduction
------------

By design asyncio `does not allow <https://github.com/python/cpython/issues/66435>`_
its event loop to be nested. This presents a practical problem:
When in an environment where the event loop is
already running it's impossible to run tasks and wait
for the result. Trying to do so will give the error
"``RuntimeError: This event loop is already running``".

The issue pops up in various environments, such as web servers,
GUI applications and in Jupyter notebooks.

This module patches asyncio to allow nested use of ``asyncio.run`` and
``loop.run_until_complete``.

Installation
------------

.. code-block::

    pip3 install git+https://github.com/ufoptg/asyncNestADV.git

Python 3.5 or higher is required.

Usage
-----

.. code-block:: python

    import nest_asyncio
    nest_asyncio.apply()
    nest_asyncio.revert()

Optionally the specific loop that needs patching can be given
as argument to ``apply``, otherwise the current event loop is used.
An event loop can be patched whether it is already running
or not. Only event loops from asyncio can be patched;
Loops from other projects, such as uvloop or quamash,
generally can't be patched.


.. |Status| image:: https://img.shields.io/badge/status-stable-green.svg
   :alt:

.. |License| image:: https://img.shields.io/badge/license-BSD-blue.svg
   :alt:

