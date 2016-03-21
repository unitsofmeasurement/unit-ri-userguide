# Data and precision management

One important part of the unit of measurement business is the possibility to make conversions.
Converting between System of unit, when all the units from a specific system (e.g. International system) are transformed to another (e.g. US system). 
Quantity scaling, when values are transformed to more appropriate scale (e.g. moving from kilometers to astronomical units).

All these requirements require that the values maintain the highest precision possible. The usage of the double primitive or the Double object, shall be avoided when precision is a requirement. 