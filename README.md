# LabVIEW-Color-Pipes

LabVIEW library to color pipes (Boolean indicators) based on one or more expressions.

## Getting Started

Clone the repository and run the `/Pipes Example.vi` to demostrate how to configure and update the pipe colors (Boolean indicators). Toggle the valves and mass flow controller (MFC) value to see the pipe colors change accordingly.

![Example](/Images/Example.png)

![Example](/Images/Example-Diagram.png)

## Usage

Pipes are Classic Flat Square Boolean Indicators, edit the pipe description to add one or more color definitions formatted as:

`x<color_hex>|<pipe_name>:[<expression>]`

If the expression is evaluated to `True` (or `!= 0`), the pipe value is set to `True` and the color is set to `<color_hex>` or the current `<pipe_name>` color.

_Note: Colors must start with 'x'. e.g. `xFFDDEE` = `FFDDEE` as RRGGBB._

If the expression is empty, the referenced `<pipe_name>:` value and color are cloned (usefull for multi-pipe segments).

Expressions can be nested using parentheses `(a or b) and (c or d)`.

Expressions can use pythonic nomenclature `(a and b or not c)` or C++ nomenclature `(a && b || !c)`.

### Expressions supported:

```
AND:          and | && | &
OR:           or | '||' | '|'
NOT:          not | !
EQUAL:        ==
NOT EQUAL:    !=
LESS THAN:    <
GREATER THAN: >
LTE:          <=
GTE:          >=
PARENTHESES:  (..)
LITERAL:      Boolean | DBL | I32 | U32
IDENTIFIER:   [A-Za-z_][A-Za-z0-9_]*
```

_Note: Bit-wise and assignment operations are not supported._

### Example Pipe Descriptions

Specify one or more color definitions by editing the pipe boolean front panel description as:

`x<color_hex>|<pipe_name>:[<expression>]`

_Note: The first expression to evaluate to True is returned. Otherwise the pipe value is set to `False` and the pipe's color is set to `gray`._

**Set pipe color (Multiple alternatives):**

```
xFFCCDD:V1 and not V2 and (MFC1 > 4.5 or V3) or V5
xDDBBAA:V3 or V4
```

**Clone value and color (No expression):**
This is useful for multi-segment pipes where only one pipe needs evaluation; the remaining pipe segments reference the parent pipe.

```
P2:            # Clone the pipe's value and color
```

**Clone color (With expression):**

```
P1:V3 or V5    # Clones a pipe's color
```

## Support

Open a ticket to bug fixes or feature requests.
