AbstractQuantity provides additional methods to convert values directly into a target unit.
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