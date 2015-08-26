Abstract Quantity
AbstractQuantity provides additional methods to convert values directly into a target unit. They are more useful as meta-data converted to the application internal representation (typically a double primitive type in some fixed units) before computation or further processing begin. For this purpose, the AbstractQuantity class provides the longValue(Unit<Q>) and doubleValue(Unit<Q>) convenience methods. For example the doubleValue(Unit<Q>) method is equivalent to the following
gg
```
public double doubleValue(Unit<Q> unit) {
   return getUnit().getConverterTo(unit).convert(getValue().doubleValue());
}
```
With such method, user code like below are slightly easier to write:
```java
double calculateTravelTimeInSeconds(Length distance, Speed speed) {
   return distance.doubleValue(METRE) /
          speed.doubleValue(METRE_PER_SECOND);
}
```
Note that an equivalent operation can also be done using the Quantity.divide(Quantity) method.