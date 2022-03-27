# Eweknits

Eweknits (pronounced "YU-nihts", i.e., "units")
is a library for creating and working with "units"
(such as feet, grams, seconds, potrzebies, etc.),
and "measures"
(such as 30 days,
9.8 meters per second per second,
364.4 smoots,
123 furlongs per fortnight,
etc.).

It provides some "base" units
(such as seconds, inches, meters, ounces avoirdupoids, and grams),
and some units made from combining them
(such as newtons, horsepower, and kilowatt-hours).


## Usage

You will probably mostly be creating and using _measures_.&nbsp;
These are created using `Eweknits.measure/2`.&nbsp;
The arguments are a numeric quantity and a `unit`.&nbsp;
For instance:

```elixir
earth_gravity = Eweknits.measure(9.8, meter_per_second_squared)
```

Once you have a `measure`, you can
add it to or subtract it from another `measure` of the same `unit`,
and multiply or divide it by another `measure` _or_ a number.&nbsp;
For instance:

```elixir
# hurl something straight down at 3.1 m/s, on the moon,
# and how fast is it going after 4.5 seconds?
# (assuming we threw it from high enough!)
moon_gravity = earth_gravity / 6
initial_velocity = Eweknits.measure(3.1, meter_per_second)
falling_time = Eweknits.measure(4.5, second)
falling_velocity = initial_velocity + moon_gravity * falling_time
```

You can also create your own units by
either just declaring it with `Eweknits.unit/1`,
or multiplying or dividing an existing unit by another unit.&nbsp;
For instance:

```elixir
newton = kilogram * meter / second / second
joule = newton * meter
watt = joule / second
```

Eweknits will automagically take care of ensuring that
the resulting measure will have the correct unit.&nbsp;
For instance, if you divide a "foot" measure by a "second" measure,
you will get a measure whose unit is "feet per second".


## Limitations / Plans

At this time it does _not_ handle
_scaled_ units
(e.g., automatic conversion between feet and inches,
let alone between feet and _meters_),
_vector_ units (such as true _velocity_ as opposed to _speed_),
nor unit _conversions_ that require an _offset_
(such as between degrees C, F, and K).&nbsp;
These features will most likely be added in that order.

It also does not yet search for extant units fitting a description.&nbsp;
So, if you do a calculation that results in, say, joules,
and print out the results,
it will print them out in terms of the base units and their exponents.&nbsp;
Eventually it _may_ search a registry for
some way to at least simplify the output.


## Installation

If [available in Hex](https://hex.pm/docs/publish), the package can be installed
by adding `eweknits` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:eweknits, "~> 0.1.0"}
  ]
end
```

Documentation can be generated with [ExDoc](https://github.com/elixir-lang/ex_doc)
and published on [HexDocs](https://hexdocs.pm). Once published, the docs can
be found at <https://hexdocs.pm/eweknits>.
