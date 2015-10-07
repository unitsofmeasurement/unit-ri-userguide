## Hurricane Wind Scale

This example shows how QuantityRange can be extended e.g. to model Hurricane categories using the Saffir–Simpson hurricane wind scale (SSHWS):
```
/**
 * @see <a href="http://en.wikipedia.org/wiki/Saffir%E2%80%93Simpson_hurricane_wind_scale">
 *      Wikipedia: Saffir–Simpson hurricane wind scale</a>
 */
public class SaffirSimpsonHurricaneWindScale extends QuantityRange<Speed>> implements Nameable {
    /**
     * The storm category
     */
    public static enum Category {
        UNKNOWN, TROPICAL_DEPRESSION, TROPICAL_STORM, ONE, TWO, THREE, FOUR, FIVE
    }

    private final Category category;

    public Category getCategory() {
        return category;
    }

    private SaffirSimpsonHurricaneWindScale(Quantity<Speed> min, Quantity<Speed> max,
                                            Category level) {
        super(min, max);
        this.category = level;
    }

    private SaffirSimpsonHurricaneWindScale(Quantity<Speed> min, Quantity<Speed> max) {
        this(min, max, UNKNOWN);
    }

    /**
     * Returns an {@code SaffirSimpsonHurricaneWindScale} with the specified values.
     *
     * @param min The minimum value for the wind scale.
     * @param max The maximum value for the wind scale.
     * @return an {@code SaffirSimpsonHurricaneWindScale} with the values present
     */
    public static SaffirSimpsonHurricaneWindScale of(Quantity<Speed> min, Quantity<Speed> max) {
        return new SaffirSimpsonHurricaneWindScale(min, max);
    }

    /**
     * Returns an {@code SaffirSimpsonHurricaneWindScale} with the specified values.
     *
     * @param min The minimum value for the wind scale.
     * @param max The maximum value for the wind scale.
     * @param cat The {@link Category} of the wind scale.
     * @return an {@code SaffirSimpsonHurricaneWindScale} with the values present
     */
    public static SaffirSimpsonHurricaneWindScale of(Quantity<Speed> min, Quantity<Speed> max,
                                                    Category cat) {
        return new SaffirSimpsonHurricaneWindScale(min, max, cat);
    }

    @Override
    public boolean hasMinimum() {
        return getMinimum() != null
                && !NONE.equals(getMinimum())
                && !(getMinimum().getUnit() == null || getMinimum().getValue() == null);
    }

    @Override
    public boolean hasMaximum() {
        return getMaximum() != null
                && !NONE.equals(getMaximum())
                && !(getMaximum().getUnit() == null || getMaximum().getValue() == null);
    }

    @Override
    public String toString() {
        return getName() + " [category=" + category + ", minimum="
                + getMinimum() + ", maximum=" + getMaximum() + "]";
    }

    @Override
    public String getName() {
        return "Saffir–Simpson hurricane wind scale";
    }
}
```

This example code shows (including US-metric conversion) how the time to evacuate can be calculated for a given storm category. It also shows how to use the Quantities class:
```
SaffirSimpsonHurricaneWindScale sts = SaffirSimpsonHurricaneWindScale.of(
  Quantities.getQuantity(39, MILES_PER_HOUR),
  Quantities.getQuantity(73, MILES_PER_HOUR), TROPICAL_STORM);
[...]
SaffirSimpsonHurricaneWindScale s5 = SaffirSimpsonHurricaneWindScale.of(
  Quantities.getQuantity(157, MILES_PER_HOUR), null, FIVE);
[...]
SaffirSimpsonHurricaneWindScale scale = s5;
Quantity<Speed> metricSpeed = scale.hasMaximum() ?
  scale.getMaximum().to(KILOMETRES_PER_HOUR) :
  scale.getMinimum().to(KILOMETRES_PER_HOUR);
Quantity<Length> l = Quantities.getQuantity(500, KILO(METRE));
Quantity<Time> timeToEvacuate = l.divide(metricSpeed).asType(Time.class);
```