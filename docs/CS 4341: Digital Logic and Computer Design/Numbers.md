# Number Systems
08/28/2025

---
- Decimal: Base 10
    - Every day usage
- Binary: Base 2
    - 1s and 0s, easy for computers
- Hex: Base 16

## Base 10
Our every day number system :hand::hand:
> $5374_{10} = 5 \times10^3+3\times10^2+7\times10^1+4\times10^0$
## Base 2
Binary numbers :computer:
> $1101_2=1\times2^3+1\times2^2+0\times2^1+1\times2^0 = 13_{10}$

*It is handy to memorize up to $2^9$*
### Binary to decimal conversion :two::arrow_right::keycap_ten:
> $11010_2$

| 16 | 8 | 4 | 2 | 1 |
| -- | - | - | - | - |
| 1  | 1 | 0 | 1 | 0 |
| 16 | 8 | 0 | 2 | 0 |

### Decimal to Binary :keycap_ten::arrow_right::two:
- Two Methods:
  - Largest power of 2 that fits

    $$
    53_{10} - 32_{10} = 21_{10}\\
    - 16_{10} = 5_{10}\\
    - 4_{10} = 1_{10}\\
    - 1_{10} = 0\\
    53_{10} =110101_2
    $$

  - Repeatedly divide by 2

    $$
    53_{10}\div2=26_{10} R\blue1 \\
    \div2=13_{10}R\blue0          \\
    \div2=6_{10}R\blue1           \\
    \div2=3_{10}R\blue0           \\
    \div2=1_{10}R\blue1           \\
    \div2=R\blue1                 \\
    =\blue{110101}_2
    $$

### Binary Values and Range
#### $N$ digit decimal number
- $10^N$ values
- $[0,10^N-1]$ range
#### $N$ digit binary number
- $2^N$ values
- $[0,2^N-1]$ range
#### $N$ digit $M$-ary number
- $M^N$ values
- $[0,M^N-1]$ range

##### Equation to convert from binary to decimal

$$
A:\{a_{N-1},a_{N-2},...a_1,1_0\}\\
A = \sum^{N-1}_{i=0}{a_i2^i}
$$

## Hexadecimal
Base 16, easily converted to binary
> $\red4\blue A \green F_{16}$ or 0x4AF

$\red{0100}\blue{1010}\green{1111}_2$

## Bits, Bytes, Nibbles
- Bit: $\blue1001011\red0$
    - $\text{\blue{msb}}$: Most significant bit
    - $\text{\red{lsb}}$: Least significant bit
- Byte: $\green{10010110}$
    - $\blue{CE}BF9A\red{D7}$

## Large powers of two :two:
- $2^{10} \rightarrow$ 1 kilo
- $2^{20} \rightarrow$ 1 mega
- $2^{30} \rightarrow$ 1 giga
- $2^{40} \rightarrow$ 1 tera
- $2^{50} \rightarrow$ 1 peta
- $2^{60} \rightarrow$ 1 exa

### Estimating powers of two
> $2^{24} \approx 2^{20} \times 2^4 \approx 16 M$

## Addition :heavy_plus_sign:
Addition is the same, just remember to carry like
in normal addition

### Overflow?
The addition of two 4 bit vales gives a 4 bit result.
- Any additional values left are *ignored.*
This is considered an **overflow**.
> $1011_2 + 0110_2 = \red1\blue{0001}$

## Signed binary numbers
### Sign / magnitude
- The $\text{\blue{msb}}$ is the sign
> 0 is + and 1 is -

$$
A = \left(-1\right)^{a_{N-1}}\sum^{N-2}_{i=0}{a_i2^i}
$$
#### Two's compliment numbers
- The $\text{\blue{msb}}$ is the sign
- Invert the unsigned number + 1
    - Only works on **unsigned** numbers
- Helps with math, since just using a sign bit messes up negative math.
> Subtraction is as simple as "taking the two's" of the second number and adding them.

#### Sign extension
It is normal to prepend $0$'s or $1$'s (depends on the sign) to the number to make it fit a certain bit size.
> $11 \rightarrow \red{00}11$

> $1011 \rightarrow \red{1111}1011$

> TODO: Add octal conversion method
