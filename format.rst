Format
=======

The HDF5 format is binary. The first 8 bytes, a.k.a. magic number, is \\211HDF\\r\\n\\032\\n.

Level 0
-------
  This is metadata about file itself.

.. mermaid::
    graph LR
        A[Start] --> B{Decision}
        B -- Yes --> C[End]
        B -- No --> D[End]

        
Level 0A
^^^^^^^^

.. mermaid::

packet-beta
title test
0-15: "Source Port"
16-31: "Destination Port"
32-63: "Sequence Number"
64-95: "Acknowledgment Number"
96-99: "Data Offset"
100-105: "Reserved"
106: "URG"
107: "ACK"
108: "PSH"
109: "RST"
110: "SYN"
111: "FIN"
112-127: "Window"
128-143: "Checksum"
144-159: "Urgent Pointer"
160-191: "(Options and Padding)"
192-255: "Data (variable length)"

  
Level 1
-------

Level 2
-------
