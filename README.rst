
METIS for Python
================

Wrapper for the METIS library for partitioning graphs (and other stuff).

This library is unrelated to PyMetis, except that they wrap the same library.
PyMetis is a Boost Python extension, while this library is pure python and will
run under PyPy and interpreters with similarly compatible ctypes libraries.

NetworkX_ is recommended for representing graphs for use with this wrapper,
but it isn't required. Simple adjacency lists are supported as well.

.. _NetworkX: http://networkx.lanl.gov/

The function of primary interest in this module is :func:`part_graph`.

Other objects in the module may be of interest to those looking to 
mangle their graph datastructures into the required format. Examples
of this include the :func:`networkx_to_metis` and :func:`adjlist_to_metis` functions.
These are automatically called by :func:`part_graph`, so there is
little need to call them manually.

See the BitBucket repository_  for updates and issue reporting.

.. _repository: http://bitbucket.org/kw/metis-python

Installation
============

It's on PyPI, so installation should be as easy as::

    pip install metis
          -or-
    easy_install metis

METIS itself is not included with this wrapper. Get it here_.

.. _here: http://glaros.dtc.umn.edu/gkhome/views/metis

Note that the shared library is needed, and isn't enabled by default
by the configuration process. Turn it on by issuing::

    make config shared=1

Your operating system's package manager might know about METIS,
but this wrapper was designed for use with METIS 5. Packages with
METIS 4 will not work.

This wrapper uses a few environment variables:

.. envvar:: METIS_DLL
This wrapper uses Python's ctypes module to interface with the METIS
shared library. If it is unable to automatically locate the library, you
may specify the full path to the library file in this environment variable.

.. envvar:: METIS_IDXTYPEWIDTH
.. envvar:: METIS_REALTYPEWIDTH
The sizes of the :c:type:`idx_t` and :c:type:`real_t` types are not
easily determinable at runtime, so they can be provided with these 
environment variables. The default value for each of these (at both compile 
time and in this library) is 32, but they may be set to 64 if desired. If 
the values do not match what was used to compile the library, Bad Things(TM) 
will occur.

Example
=======

    >>> import networkx as nx
    >>> import metis 
    >>> G = metis.example_networkx()
    >>> (edgecuts, parts) = metis.part_graph(G, 3)
    >>> colors = ['red','blue','green']
    >>> for i, p in enumerate(parts):
    ...     G.node[i]['color'] = colors[p]
    ... 
    >>> nx.write_dot(G, 'example.dot') # Requires pydot or pygraphviz

.. graphviz:: example.dot

