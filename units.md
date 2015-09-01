
## Units

The <code>Units</code> class extends <code>AbstractSystemOfUnits</code> and provides a set of  a set of static constants for the most common units defined by SI/BIPM. is also provided for obtaining multiples or submultiples of system units. Method names mirror SI / Metric prefix names but are uppercase. Examples:
Unit<Length> m  = Units.METRE;
Unit<Length> km = MetricPrefix.KILO(Units.METRE);
Unit<Energy> kW = MetricPrefix.KILO(Units.WATT);
Unit instances returned by one of these methods provide type safety through unit parameterization (the <Length> and <Energy> type parameters). This feature was discussed previously in Unit Parametrization.

