# Pdv
A mini pattern language for creating patterns of durations and values. The syntax was inspired by the mini notaion of TidalCycles but not intended as an exact copy or port of it.

## Installation

```
Quarks.install("https://github.com/dmorgan-github/Pdv")
thisProcess.recompile
```

## Syntax

```
" "    - empty space separates beats/values
~      - rest
[]     - beat sub division or group
<>     - alternating values
{}     - chord values
^n     - stretch duration - where n is a float
!n     - repeat value - where n is an integer
$      - shuffle group of values
?n     - chance of value or rest - optional probability is specified with n as an integer 0-9
#(nnn) - choose one value from preceeding group of values, optional weights are specified within parens where n is an integer 0-9
|      - can be used as visual separator to help readability
,      - can be used as visual separator to help readability
```

## Example

Here is a somewhat convoluted example. But it should be apparent that operators can be combined in interesting ways to create complex sequences which would be cumbersome to create with the usual Pattern classes.

```
~p = Pbind(\degree, Pdv.parse("0 <1?4 2?8> [7 6 5 4]$ {3 [4 5]# <6 8>}")).asStream;
~p.nextN(15, Event.default).do({|v| v.postln;})
( 'degree': 0.0, 'dur': 1.0, 'g1': true )
( 'degree': rest, 'dur': Rest(1.0) )
( 'degree': 4.0, 'dur': 0.25 )
( 'degree': 7.0, 'dur': 0.25 )
( 'degree': 5.0, 'dur': 0.25 )
( 'degree': 6.0, 'dur': 0.25 )
( 'degree': [ 3.0, 5.0, 6.0 ], 'dur': 1.0 )
( 'degree': 0.0, 'dur': 1.0, 'g1': true )
( 'degree': 2.0, 'dur': 1.0 )
( 'degree': 6.0, 'dur': 0.25 )
( 'degree': 7.0, 'dur': 0.25 )
( 'degree': 5.0, 'dur': 0.25 )
( 'degree': 4.0, 'dur': 0.25 )
( 'degree': [ 3.0, 4.0, 8.0 ], 'dur': 1.0 )
```




