# Library

The JSR 363 Reference Implementation uses the **Common** module of [UoM Library](https://github.com/unitsofmeasurement/uom-lib) 
The following elements are defined in UoM Common Library to be platform-independent working under Java ME 8 as well as Java SE.
## Parser
A function that parses an input value and produces an output. This general purpose parser is used by AbstractUnitFormat or QuantityFormat but can also offer its functional interface to other parsers, e.g. UCUM, oBIX, JSON, XML or similar parsing purposes.
