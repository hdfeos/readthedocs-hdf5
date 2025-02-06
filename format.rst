Format
=======

The HDF5 format is binary. The first 8 bytes, a.k.a. magic number, is \\211HDF\\r\\n\\032\\n.

The default *k* value of version 1 B-tree

* chunk indices: 32
* group symbol tables
  * internal nodes: 16
  * leaf node: 4

Level 0
-------
  This is metadata about file itself.

.. mermaid:: l0.mmd

        
Level 0A
^^^^^^^^

.. mermaid:: p.mmd

  
Level 1
-------

Level 2
-------
