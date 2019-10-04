.. _Chemical_Markup_Language:

Chemical Markup Language (cml, mrv)
===================================

**An XML format for interchange of chemical information.**


This format writes and reads CML XML files. To write CML1 format rather than
the default CML2, use the ``-x1`` option. To write the array form use ``-xa``
and to specify all hydrogens using the hydrogenCount attribute on atoms use
``-xh``.

Crystal structures are written using the <crystal>, <xfract> (,...etc.)
elements if the OBMol has a OBGenericDataType::UnitCell data.

All these forms are handled transparently during reading. Only a subset of
CML elements and attributes are recognised, but these include most of those
which define chemical structure, see below.

The following are read:

- Elements:

  - molecule, atomArray, atom, bondArray, bond, atomParity, bondStereo
  - name, formula, crystal, scalar (contains crystal data)
  - string, stringArray, integer, integerArray, float floatArray, builtin

- Attributes:

  - On <molecule>: id, title, ref(in CMLReact)
  - On <atom>: id, atomId, atomID, elementType, x2, y2, x3, y3, z3, xy2, xyz3,
    xFract, yFract, zFract, xyzFract, hydrogenCount, formalCharge, isotope,
    isotopeNumber, spinMultiplicity, radical(from Marvin),
    atomRefs4 (for atomParity)
  - On <bond>: atomRefs2, order, CML1: atomRef, atomRef1, atomRef2

Atom classes are also read and written. This is done using a specially
formed atom id. When reading, if the atom id is of the form aN_M (where
N and M are positive integers), then M is interpreted as the atom class.
Such atom ids are automatically generated when writing an atom with an
atom class.



Read Options
~~~~~~~~~~~~ 

-2  *read 2D rather than 3D coordinates if both provided*


Write Options
~~~~~~~~~~~~~ 

-1  *write CML1 (rather than CML2)*
-a  *write array format for atoms and bonds*
-A  *write aromatic bonds as such, not Kekule form*
-m  *write metadata*
-x  *omit XML and namespace declarations*
-c  *continuous output: no formatting*
-p  *write properties*
-N <prefix>  *add namespace prefix to elements*


Comments
~~~~~~~~
In the absence of hydrogenCount and any explicit hydrogen on
an atom, implicit hydrogen is assumed to be present appropriate
to the radical or spinMultiplicity attributes on the atom or
its normal valency if they are not present.

The XML formats require the XML text to be well formed but
generally interpret it fairly tolerantly. Unrecognised elements
and attributes are ignored and there are rather few error messages
when any required structures are not found. This laxity allows, for
instance, the reactant and product molecules to be picked out of a CML
React file using CML. Each format has an element which is regarded as
defining the object that OpenBabel will convert. For CML this is
<molecule>. Files can have multiple objects and these can be treated
the same as with other multiple object formats like SMILES and MDL
Molfile. So conversion can start at the nth object using the ``-fn`` option
and finish before the end using the ``-ln`` option. Multiple object XML files
also can be indexed and searched using FastSearch, although this has
not yet been extensively tested.

