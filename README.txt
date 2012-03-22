METIS for Python
================

Wrapper for the METIS library for partitioning graphs (and other stuff).

This library is unrelated to PyMetis, except that they wrap the same library.
PyMetis is a Boost Python extension, while this library is pure python and will
run under PyPy and interpreters with similarly compatible ctypes libraries.

The functions of primary interest are:

    `metis.part_graph_kway`
    `metis.part_graph_recur`

They are also the only objects export by "from metis import *".
Other objects in the module may be of interest to those looking to 
mangle their graph datastructures into the required format. Examples
of this include the `networkx_to_metis` and `adjlist_to_metis` functions.
These are automatically called by the `part_graph_` functions, so there is
little need to call them manually.

See the repository_ for updates and issue reporting.

Installation
============

It's on PyPI, so installation should be as easy as::

    pip install metis
          -or-
    easy_install metis

METIS itself is not included with this wrapper. Get it here_.

Note that the shared library is needed, and isn't enabled by default
by the configuration process. Turn it on by issuing:
    
    make config shared=1

Your operating system's package manager might know about METIS,
but this wrapper was designed for use with METIS 5. Packages with
METIS 4 will probably not work.

This wrapper uses Python's ctypes module to interface with the METIS
shared library. If it is unable to automatically locate the library, you
may specify the full path to the library file in the METIS_DLL environment
variable.

Additionally, there are a few compile options that you may need to tell
the wrapper about. The sizes of the "idx_t" and "real_t" types are not
easily determinable at runtime, so they can be provided with the 
environment variables METIS_IDXTYPEWIDTH and METIS_REALTYPEWIDTH.
The default value for each of these (at both compile and in this library)
is 32, but they may be set to 64 if desired. If the values do not match
what was used to compile the library, Bad Things™ will occur.

.. _here: http://glaros.dtc.umn.edu/gkhome/views/metis
.. _repository: http://bitbucket.org/kw/metis-python
