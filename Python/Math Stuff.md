# Math Stuff

## Math Library Functions

---

| **Math Function** | **Description** |
| --- | --- |
| `Math.ceil` | Rounds up the value |
| `Math.fabs` | Absolute value |
| `Math.factorial` | Factorial |
| `Math.floor` | Rounds down the value |
| `Math.fmod` | Remainder of division |
| `Math.fsum` | Floating-point sum |
| `Math.exp` | The exponential function (`e^x`) |
| `Math.log` | Natural log |
| `Math.pow` | Raise to a power |
| `Math.sqrt` | Square root |
| `Math.acos` | Arc cosine (inverse cosine) |
| `Math.asin` | Arc sine (inverse sine) |
| `Math.atan` | Arc tangent (inverse tangent) |
| `Math.atan2` | Arc tangent with two parameters |
| `Math.cos` | Cosine |
| `Math.sin` | Sine |
| `Math.tan` | Tangent |
| `Math.hypot` | Length of a vector from its origin |
| `Math.degrees` | Converts radians to degrees |
| `Math.radians` | Converts degrees to radians |
| `Math.cosh` | Hyperbolic cosine |
| `Math.sinh` | Hyperbolic sine |
| `Math.gamma` | The gamma function |
| `Math.erf` | The error function |
| `Math.pi` | Value of pi |
| `Math.e` | Value of e |

## Mathematical Operators

---

Python supports compound operators to quickly update the value of a variable

- `+=`, `-=`, `*=`, `/=`, `%=`

Modulo operator `%` evaluates remainder of division of two integer inputs

- Example:

        24 % 10 = 24/10 with remainder = 2 remainder 4 = 4

Floored division operator `//` will divide a number by another number and round to the nearest whole value

- Example: `57 // 9 = 6`
- Example: `52 // 10 = 5`
- Example: `40 // 42 = 0`

Modulo and floored division can be used to retrieve any amount of digits from an integer

- Example: `` `any integer` % 10 = `the last digit of the integer` ``
- Example: `` `any integer` % 100 = `the last two digits of the integer` ``
- Example: `` `any integer` // 10`` shifts the decimal one place to the left
- Example: `` `any integer` // 100`` shifts the decimal two places to the left

## Other Math Stuff

To generate a random integer, use the function `random.randint()` and pass two integers as the inclusive lower and upper bounds

- Need to import random library first

**Binary numbers**: each positive integer can be represented by a uniform linear combination of 2's raised to positive integer powers

- 8 digits (bits) is the most typically included in a string, and 255 is the largest number that can be created with 8 bits (all powers of 2 included)
- Example:

        01001101 = 0*(2^7) + 1*(2^6) + 0*(2^5) + 0*(2^4) + 1*(2^3) + 1*(2^2) + 0*(2^1) + 1*(2^0) = 64 + 8 + 4 +1 = 77
