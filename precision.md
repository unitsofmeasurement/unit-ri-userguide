# Preserving precision

When working with measure, one mandatory aspect is the ability to maintain the precision: in operations, in conversions.
For example conversion between System of unit (e.g. SI to US system) or scaling (e.g. moving from kilometers to astronomical units).

```Uom-se``` supports conversions using Double (and double primitive) and Number. 
The recommendation is **not to use Double** but to use BigDecimal, which is a type designed is required to preserve precision for very big or very small numbers. From the Javadoc of BigDecimal: 

> Immutable, arbitrary-precision signed decimal numbers. A BigDecimal consists of an arbitrary precision integer unscaled value and a 32-bit integer scale. If zero or positive, the scale is the number of digits to the right of the decimal point. If negative, the unscaled value of the number is multiplied by ten to the power of the negation of the scale.

**Note**: the safest and correct approach to create a BigDecimal is to use the contructor accepting String. Using the constructor that require double will create the BigDecimal object from a incorrect form, leading to the same problems affecting the Double object representation. 

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

