
## Quantities

The reference implementation provides a singleton factory accessor class <code>Quantities</code>, like <code>Collections</code> and other similar classes in the JDK. This class is a “convenience” facade over having to retrieve a new instance of <code>QuantityFactory</code> via the SPI for obtaining new Quantity instances. Examples:
```
Qantity<Time> t = Quantities.getQuantity(12, MILLI(SECOND));
Quantity<Length> len = Quantities.getQuantity(34.5, MILE);
```