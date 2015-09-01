
## Units

The <code>Units</code> class extends <code>AbstractSystemOfUnits</code> and provides a set of  a set of static constants for the most common units defined by SI/BIPM. is also provided for obtaining multiples or submultiples of system units. Method names mirror SI / Metric prefix names but are uppercase. Examples:
```
Unit<Length> m  = Units.METRE;
Unit<Length> km = MetricPrefix.KILO(Units.METRE);
Unit<Energy> kW = MetricPrefix.KILO(Units.WATT);
```
Unit instances returned by one of these methods provide type safety through unit parameterization (the <Length> and <Energy> type parameters). This feature was discussed in the [Unit Parametrization ](https://docs.google.com/document/d/12KhosAFriGCczBs6gwtJJDfg_QlANT92_lhxUWO2gCY/edit#heading=h.bhjpzpqftc5g)chapter of the specification.

