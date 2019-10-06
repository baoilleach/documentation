.. _ChemDraw_binary_format:

ChemDraw binary format (cdx)
============================

**Read only**

The whole file is read in one call.
Note that a file may contain a mixture of reactions and
molecules.
With the -ad option, a human-readable representation of the CDX tree
structure is output as an OBText object. Use textformat to view it::

    obabel input.cdx -otext -ad

Many reactions in CDX files are not fully specified with reaction data
structures, and may not be completely interpreted by this parser.



.. note:: This is a read-only format.

Read Options
~~~~~~~~~~~~ 

-m  *read molecules only; no reactions*
-d  *output CDX tree to OBText object*
-o  *display only objects in tree output*
