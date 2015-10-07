## Using Enums

The enum type is final, so it works better for a smaller set of well-known elements. The fact, that NONE (Dimensionless) has no symbol but a default unit made it harder to deal with enums and their default constructors. A default yet extensible model and dimensional calculations made it even harder..
Enums are used in some areas, e.g. behavior of parsing and formatting or unit prefixes. In most other parts of the API we need to keep it open and flexible towards extensions. Which a final type like enum wouldn't work for. In cases where a quantity implementation shall be final and values would be a selection of  choices rather than a numeric value, using enums to implement such quantity seems tempting. Using interfaces to interconnect different but related sets of enums is suggested by . It works in various practical frameworks EG members worked on. And looking at restrictions some already final JSRs are bound to by their use of enums lets one hope its next releases find alternatives here, too.
The following example of how to use unit declarations instead of primitive or simple Number objects was based on code from the Enums chapter in [EFFECTIVEJAVA] (p. 150ff)

import javax.measure.quantity.Length;
import javax.measure.quantity.Mass;
import javax.measure.Unit;

import static tec.units.ri.unit.Units.METRE;
import static tec.units.ri.unit.Units.KILOGRAM;

public enum Planet {
	 MERCURY (KILOGRAM.multiply(3.303e+23), METRE.multiply(2.4397e6)),
	 VENUS   (KILOGRAM.multiply(4.869e+24), METRE.multiply(6.0518e6)),
	 EARTH   (KILOGRAM.multiply(5.976e+24), METRE.multiply(6.37814e6)),
	 MARS    (KILOGRAM.multiply(6.421e+23), METRE.multiply(3.3972e6)),
	 JUPITER (KILOGRAM.multiply(1.9e+27),   METRE.multiply(7.1492e7)),
	 SATURN  (KILOGRAM.multiply(5.688e+26), METRE.multiply(6.0268e7)),
	 URANUS  (KILOGRAM.multiply(8.686e+25), METRE.multiply(2.5559e7)),
	 NEPTUNE (KILOGRAM.multiply(1.024e+26), METRE.multiply(2.4746e7)),

	 private final Unit<Mass> mass;   // in kilograms
	 private final Unit<Length> radius; // in meters

	 Planet(Unit<Mass> mass, Unit<Length> radius) {
	        this.mass = mass;
	        this.radius = radius;
	 }

   public Unit<Mass> mass()   { return mass; }
	  public Unit<Length> radius() { return radius; }
   [...]
}
Note, Pluto is missing (contrary to [EFFECTIVEJAVA] unless the author corrected this in later editions) since it isn’t considered a planet any more. UoM demos contain a similar enum DwarfPlanet including Pluto and other dwarf planets discovered so far.