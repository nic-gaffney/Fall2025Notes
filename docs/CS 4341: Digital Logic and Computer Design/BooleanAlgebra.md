# Boolean Algebra
09/09/2025

---
## Introduction
A logic circuit is composed of:

- inputs
- outputs
- functional specification
- timing specification

## Types of logic circuits
- Combinational logic
  - Memoryless
  - Outputs determined by *current value* of inputs
- Sequential logic
  - Memory
  - Outputs determined by **previous** and current value of inputs

### Rules of combinational composition
- Every element is combinational
- Every note is either input or output
- No cyclic paths
> Inputs are only inputs, outputs are only outputs

## Boolean Equations
- Functional specification of outputs in terms of inputs
> Adder example: <br>
$S=F(A,B,C_{in})$ <br>
$C_{out}=F(A,B,C_{in})$ <br>
$S=A \oplus B \oplus C$ <br>
$C_{out}=AB + AC_{in} + BC_{in}$

#### Definitions
- **Compliment**: Variable with bar over it: $\overline A$
- **Literal**: Varialbe or its *compliment*: $\overline{A}$
- **Implicant**: Product of *literals*
- **Minterm**: Product that includes all input variables
- **Maxterm**: Sum that includes all input variables

### Sum of products
- All boolean equations can be written in **SOP** form
- Each row has a *minterm*
- A minterm is a **product** of literals
- Each minterm is **TRUE** for that row
- Form function by **ORing minterms** where **output is 1**
- Thus, a $\text{\blue{sum}}$ of $\text{\red{products}}$
- $Y = F(A,B) = \red {\overline A B} \blue + \red{AB} = \sum(1,3)$

| A B | Y | Minterm | Minterm name |
| --- | - | ------- | ------------ |
| 0 0 | 0 | $\overline AB$ | $m_0$ |
| 0 1 | 1 | $\overline AB$ | $m_1$ |
| 1 0 | 0 | $A\overline B$ | $m_2$ |
| 1 1 | 1 | ${AB}$         | $m_3$ |

### Product of sums
- All boolean equations can be written in **POS** form
- Each row has a **maxterm**
- A maxterm is a **sum** of literals
- Each maxterm is **FALSE** for that row
- Form function by **ANDing maxterms** where **output is 0**
- Thus, a $\text{\blue{product}}$ of $\text{\red{sums}}$
- $Y = F(A,B) = \red {(A + B)} \blue \times \red{(\overline A + B)} = \Pi(0,2)$


| A B | Y | Maxterm | Maxterm name |
| --- | - | ------- | ------------ |
| 0 0 | 0 | $A + B$ | $M_0$ |
| 0 1 | 1 | $A + \overline B$ | $M_1$ |
| 1 0 | 0 | $\overline A + B$ | $M_2$ |
| 1 1 | 1 | ${\overline A + \overline B}$ | $M_3$ |

### Examples
#### Boolean equations
You are going for lunch.

- You wont eat $E=0$
- if cafeteria is not open $O=0$ or
- if they only serve corndogs $C=1$

##### SOP
$E = O\overline{C} = \sum(2)$ <br>
Draw the table

| O C | E | Minterm        |
| --- | - | -------        |
| 0 0 | 0 | $\overline OC$ |
| 0 1 | 0 | $\overline OC$ |
| 1 0 | 1 | $O\overline C$ |
| 1 1 | 0 | ${OC}$         |


##### POS
$E = (O + C)(O + \overline C)(\overline O + \overline C) = \Pi(0,1,3)$ <br>
Draw the table

| O C | E | Maxterm                         |
| --- | - | -------                         |
| 0 0 | 0 | $O + C$                         |
| 0 1 | 0 | $O + \overline C$               |
| 1 0 | 1 | $\overline O + C$               |
| 1 1 | 0 | ${\overline O + \overline C}$   |


### Boolean Axioms
| Number | Axiom | Dual |    Name |
| ------ | ----- | ----- |   ----- |
| A1 | Item2.1   | Item3.1 | Item3.1 |
| A2 | $0=1$   | Item3.2 | Item3.2 |
| A3 | $0\times0=0$   | Item3.3 | Item3.3 |
| A4 | $1\times1=1$   | Item3.4 | Item3.4 |
| A5 | $0\times1 = 1\times0 = 0$   | Item3.4 | Item3.4 |

> dual: Replace $\cdot$ with + and 0 with 1

### Boolean theorems of One
| Number | Theorem | Dual |    Name |
| ------ | ----- | ----- |   ----- |
| T1 | $B\times1=B$   | $B + 0 = B$ | Identity |
| T2 | $B\times0=0$   | $B + 1 = 1$ | Null Element |
| T3 | $\overline B\times B=B$   | $B + B = B$ | Idempotency |
| T4 | $B = \overline\overline B$    | | Involution |
| T5 | $B\times B = B$   | $B + \overline B = 1$ | Complements |

#### Identity theorem
- $B\times 1 = B$
- $B + 0 = B$

#### Null Element theorem
- $B\times 0 = 0$
- $B + 1 = 1$

#### Idempotency Element theorem
- $B\times B = B$
- $B + B = B$

#### Involution Element theorem
- $\overline\overline B = B$

#### Compliment theorem
- $B\times \overline B = 0$
- $B + \overline B = 1$
