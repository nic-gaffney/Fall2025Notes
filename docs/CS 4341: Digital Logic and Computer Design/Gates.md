# Logic Gates
09/02/2025

---
> Focus of this course is on Logic (*adders / memories*) and digital circuits (*AND gates, NOT gates*.)
## Background
Semiconductor industry grew from 21 billion in 1985 to 306 billion in 2016.
We went from vaccum tubes to silicon for semiconductors.

## Semiconductor Tech
- Silicon: Semiconductor
- Add material to transform properties:
    - Conductors
    - Insulators
    - Switches

## The art of managing
- Abstraction
- Discipline
- Three Y's
    - Heirarch**y**
    - Modularit**y**
    - Regularit**y**

### Discipline
- Intentionally restrict design choices
- Digital absraction considers discrete subsets of values
- **Two discrete values**
    - 1 = TRUE = HIGH
    - 0 = FALSE = LOW

## Logic gates
### NOT
$Y=\not{A}$

| A | Y |
| - | - |
| 0 | 1 |
| 1 | 0 |

### AND
$Y=AB$

| A | B | Y |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

### OR
$Y=A+B$

| A | B | Y |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

### NAND
$Y=\not{AB}$

| A | B | Y |
| - | - | - |
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

### NOR
$Y=\not{A+B}$

| A | B | Y |
| - | - | - |
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

#### XOR
$Y=A\xor B$

| A | B | Y |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

#### XNOR
$Y=\not{A\xor B}$

| A | B | Y |
| - | - | - |
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

### Multiple input Logic gates
#### NOR3
$Y=\not{A + B + C}$

| A | B | C | Y |
| - | - | - | - |
| 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 0 |

#### AND
$Y=ABC$

| A | B | C | Y |
| - | - | - | - |
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 1 |

#### XOR3
$Y=\not{A + B + C}$

Odd parity: The output is 1 when an odd number of inputs is 1

| A | B | C | Y |
| - | - | - | - |
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 1 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 1 |

## Logic levels
- Discrete voltages represent 1 and 0
- 0 is Ground (GND)
- 1 = $V_{DD}$ or 5 volts
> what about 4.99? What about 3.2? :question:
### Noise
- Anything that degrates the signal is noise.
> A gate outputs 5V but due to resistance in a long wire the reciever gets 4.5V

Noise margins: There is a range of voltages for the input and the output that
is accepted for a 1 or 0

$NM_H=V_{OH}-V_{IH}$<br>
$NM_L=V_{IL}-V_{OL}$
