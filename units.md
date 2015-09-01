
## Units

The <code>Units</code> class extends <code>AbstractSystemOfUnits</code> and provides a set of  a set of static constants for the most common units defined by SI/BIPM, see [link text](http://...#abcd) . 

## Metric Prefix
<code>MetricPrefix</code> is provided for obtaining multiples or submultiples of system units. Method names mirror SI / Metric prefix names but are uppercase like it's common to **constants** in Java. <code>MetricPrefix</code> is a "hybrid" enum, defining the constant factors as enumeration elements, but doing the actual conversion via matching static method names like <code>CENTI</code>, <code>MEGA</code>, etc. 

Examples:
```
Unit<Length> m  = Units.METRE;
Unit<Length> km = MetricPrefix.KILO(Units.METRE);
Unit<Energy> kW = MetricPrefix.KILO(Units.WATT);
```
Unit instances returned by one of these methods provide type safety through unit parameterization (the <Length> and <Energy> type parameters). This feature was discussed in the [Unit Parametrization ](https://docs.google.com/document/d/12KhosAFriGCczBs6gwtJJDfg_QlANT92_lhxUWO2gCY/edit#heading=h.bhjpzpqftc5g)chapter of the specification.

