
METIS for Python
================

Wrapper for the METIS library for partitioning graphs (and other stuff).

This library is unrelated to PyMetis, except that they wrap the same library.
PyMetis is a Boost Python extension, while this library is pure python and will
run under PyPy and interpreters with similarly compatible ctypes libraries.

NetworkX_ is recommended for representing graphs for use with this wrapper,
but it isn't required. Simple adjacency lists are supported as well.

.. _NetworkX: http://networkx.lanl.gov/

Please see the full documentation_ for examples or the BitBucket repository_ for bug reports

.. _documentation: http://metis.readthedocs.org
.. _repository: https://bitbucket.org/kw/metis-python
