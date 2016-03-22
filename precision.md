# Preserving precision

When managing measures, preserving precision is an important aspect to consider. The ability to maintain the precision is crucial when numbers are big or small. Operation of quantities having small rounding errors could accumulate and lead to wrong results.  

```Uom-se``` supports conversions using double and Number. The recommendation is to use BigDecimal and **avoid Double** (see example below). 

BigDecimal has been designed to store and manipulate big or very small numbers. A brief technical introduction can be found in the Javadoc: 
> Immutable, arbitrary-precision signed decimal numbers. A BigDecimal consists of an arbitrary precision integer unscaled value and a 32-bit integer scale. If zero or positive, the scale is the number of digits to the right of the decimal point. If negative, the unscaled value of the number is multiplied by ten to the power of the negation of the scale.

**Note**: the safest and correct approach to create a BigDecimal is to use the contructor accepting String. **Avoid** the constructor requiring double parameter as will construct the object from a incorrect form. This lead to the same problems affecting the double object representation. 

Here an example of loss of precision: 
```
UnitFormatService formatService = Bootstrap.getService(UnitFormatService.class);
UnitFormat defaultFormatService = formatService.getUnitFormat();

TransformedUnit unit = (TransformedUnit) defaultFormatService.parse("g");
System.out.println("Conversion using double: " + unit.getSystemConverter().convert(0.39));
System.out.println("Conversion using BigDecimal: " + (unit.getSystemConverter().convert(new BigDecimal("0.39"))));
System.out.println("Conversion using BigDecimal output Double: " + new BigDecimal(unit.getSystemConverter().convert(new BigDecimal("0.39")).toString()).doubleValue());

unit = (TransformedUnit) defaultFormatService.parse("%");
System.out.println("Conversion using double: " + unit.getSystemConverter().convert(0.009));
System.out.println("Conversion using BigDecimal: " + (unit.getSystemConverter().convert(new BigDecimal("0.009"))));
System.out.println("Conversion using BigDecimal output Double: " + new BigDecimal(unit.getSystemConverter().convert(new BigDecimal("0.009")).toString()).doubleValue());
```

The result is the following: 
```
Conversion using double: 3.9E-4
Conversion using BigDecimal: 0.00039
Conversion using BigDecimal output Double: 3.9E-4
Conversion using double: 8.999999999999999E-5
Conversion using BigDecimal: 0.00009
Conversion using BigDecimal output Double: 9.0E-5
```

To read more about BigDecimal there are several resources: 
- https://docs.oracle.com/javase/8/docs/api/index.html?java/math/BigDecimal.html
- http://stackoverflow.com/questions/322749/retain-precision-with-double-in-java

