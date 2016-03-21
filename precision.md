# Data and precision management

One important part of the unit of measurement business is the possibility to make conversions:
 - Conversion between System of unit (e.g. SI to US system). 
 - Scaling, when values are transformed to more appropriate scale (e.g. moving from kilometers to astronomical units).

Uom-se supports both double/Double and Number. As a best practice the usage of double primitive or the Double object should be avoided, especially if the data is used for arithmetic operations. 

We recommend to use always BigDecimal: 

> Immutable, arbitrary-precision signed decimal numbers. A BigDecimal consists of an arbitrary precision integer unscaled value and a 32-bit integer scale. If zero or positive, the scale is the number of digits to the right of the decimal point. If negative, the unscaled value of the number is multiplied by ten to the power of the negation of the scale.

**Note**: the use of the BigDecimal(String number) constructor is the safest and correct approach (the constructor that require double, is creating the BigDecimal from a incorrect form, for certain numbers). 

Here an example of loss of precision: 
```
UnitFormatService formatService = Bootstrap.getService(UnitFormatService.class);
UnitFormat defaultFormatService = formatService.getUnitFormat();

TransformedUnit unit = (TransformedUnit) defaultFormatService.parse("g");
System.out.println("Conversion using double: "+unit.getSystemConverter().convert(0.39));
System.out.println("Conversion using BigDecimal: "+(unit.getSystemConverter().convert(new BigDecimal("0.39")));

unit = (TransformedUnit) defaultFormatService.parse("%");
System.out.println("Conversion using double: "+unit.getSystemConverter().convert(0.009));
System.out.println("Conversion using BigDecimal: "+(unit.getSystemConverter().convert(new BigDecimal("0.009"))
```

The result is the following: 
```
Conversion using double: 3.9000000000000005E-4
Conversion using BigDecimal: 0.00039
Conversion using double: 8.999999999999999E-5
Conversion using BigDecimal: 0.00009
```


To know more about BigDecimal there are several resources: 
- https://docs.oracle.com/javase/8/docs/api/index.html?java/math/BigDecimal.html
- http://stackoverflow.com/questions/322749/retain-precision-with-double-in-java

