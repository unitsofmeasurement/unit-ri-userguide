
# Abstract Base Classes

The reference implementation contains a range of abstract base classes for every
vital element defined by the JSR 363 API.

While some JSRs offer abstract base classes in their public API, 
most of them are specialized to their target environment 
(Java Embedded and ME Embedded in case of the RI) so having them as part of the 
implementation makes it easier to scale or optimize for other environments in a
different implementation. 

E.g. an alternate implementation (not the RI) [for Java SE 8 and above](https://github.com/unitsofmeasurement/uom-se) could use Lambda 
expressions or new classes introduced by Java 8 while the RI won't do this 
unless they become available in Java ME Embedded, too.