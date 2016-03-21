# Data and precision management

One important part of the unit of measurement business is the possibility to make conversions:
 - Conversion between System of unit (e.g. SI to US system). 
 - Scaling, when values are transformed to more appropriate scale (e.g. moving from kilometers to astronomical units).

Uom-se supports both double/Double and Number. As a best practice the usage of double primitive or the Double object should be avoided, especially if the data is used for arithmetic operations. 

We recommend to use always BigDecimal, as shown in the example below: 
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



