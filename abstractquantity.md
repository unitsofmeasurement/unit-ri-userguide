# AbstractQuantity

<code>AbstractQuantity</code> provides additional methods to convert values directly into a target unit. They are more useful as meta-data converted to the application's internal representation (typically a double primitive type in some fixed units) before computation or further processing begin.
For this purpose <code>AbstractQuantity</code> provides the <code>longValue(Unit< Q >)</code> and <code>doubleValue(Unit< Q >)</code> convenience methods. 

For example the <code>doubleValue(Unit< Q >)</code> method is equivalent to the following:
```
public double doubleValue(Unit<Q> unit) {
   return getUnit().getConverterTo(unit).convert(getValue().doubleValue());
}
```
With such method, user code like below are slightly easier to write:
```java
double calculateTravelTimeInSeconds(AbstractQuantity<Length> distance, AbstractQuantity<Speed> speed) {
   return distance.doubleValue(METRE) /
          speed.doubleValue(METRE_PER_SECOND);
}
```
Note that an equivalent operation can also be done using the Quantity.divide(Quantity) method.