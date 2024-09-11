
# Sample MD form Git Client

## Code

The simplest way to use `revert` is without providing a reason for the revert.

```solidity!
contract ContractA {
    function mint() external pure {
        revert();
    }
}
```

If we deploy the above contract (`ContractA`) and perform a low-level call to the `mint()` function from another contract (`ContractB`) like so:

```solidity!
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

import "hardhat/console.sol";

contract ContractB {
    function call_failure(address contractAAddress) external {
        (, bytes memory err) = contractAAddress.call(
            abi.encodeWithSignature("mint()")
        );

        console.logBytes(err);
    }
}
```

The `revert()` error will be triggered no data will be returned, as shown in the screenshot below:

![revert with no error string return data in hexadecimal format: 0x](https://static.wixstatic.com/media/706568_56c8fed0267e4f0caa75b2f6a3b1a127~mv2.png/v1/fill/w_666,h_400,al_c,q_85,usm_0.66_1.00_0.01,enc_auto/706568_56c8fed0267e4f0caa75b2f6a3b1a127~mv2.png)

In the image above, we can see that the return data from the error is `0x` which is just a hexadecimal notation without accompanying data.


## Table

The table below shows how Boolean circuits and arithmetic circuits differ, but keep in mind they serve the same purpose of validating a witness:

| Boolean Circuit | Arithmetic Circuit |
| --- | --- |
| Variables are 0, 1 | Signals hold numbers |
| The only operations are AND, OR, NOT | The only operations are addition and multiplication |
| Satisfied when the output is true | Satisfied when the left hand side equals the right hand side for all equations (there is no output) |
| Witness is an assignment to the Boolean variables that satisfies the Boolean circuit | Witness is an assignment to the signals that satisfies all the equality constraints |

Aside from the convenience of using fewer variables in some circumstances, arithmetic circuits and Boolean circuits are tools that accomplish the same job — proving you have a witness to a problem in NP.


## List

For example, if we want to express $a + b = c$ where $a = 8, b = 4, c = 12$ we must transform $a$, $b$, and $c$ into binary numbers. Each bit in the binary number will correspond to a distinct Boolean variable. In this example, let's assume we need 4 bits to encode $a$, $b$, and $c$, where $a₀$ represents the Least Significant Bit (LSB), and $a₃$ represents the Most Significant Bit (MSB) of number $a$, as shown below:

- `a₃, a₂, a₁, a₀`
  - $a = 1000$
- `b₃, b₂, b₁, b₀`
  - $b = 0100$
- `c₃, c₂, c₁, c₀`
  - $c = 1100$

## Mathjak


## Sample dari ZK Inner 
- https://github.com/RareSkills/zk-book/blob/prod/content/zk-inner-product/en/zk-inner-product.md

## Polynomials with vectors as coefficients
The following are two polynomials with vector coefficients:

$$
\begin{align*}
\mathbf{l}(x) &= \begin{bmatrix} 1 \\ 2 \end {bmatrix} x + \begin{bmatrix} 3 \\ 4 \end{bmatrix} \\
\mathbf{r}(x) &= \begin{bmatrix} 2 \\ 3 \end{bmatrix} x +\begin{bmatrix} 7 \\ 2 \end{bmatrix}
\end{align*}
$$

Evaluating a vector polynomial produces another vector. For example, $\mathbf{l}(2)$ produces

$$
\mathbf{l}(2) = \begin{bmatrix} 1 \\ 2 \end{bmatrix} (2) + \begin{bmatrix} 3 \\ 4 \end{bmatrix} = \begin{bmatrix} 5 \\ 8 \end{bmatrix}
$$


and evaluating $\mathbf{r}$ at 2 returns:

$$
\mathbf{r}(2) = \begin{bmatrix} 2 \\ 3 \end{bmatrix} (2) + \begin{bmatrix} 7 \\ 2 \end{bmatrix} = \begin{bmatrix} 11 \\ 8 \end{bmatrix}
$$

## Multiplying vector polynomials
Vector polynomials can be multiplied together like scalar polynomials. For example, multiplying $\mathbf{l}(x)$ and $\mathbf{r}(x)$ yields:

$$
\mathbf{l}(x)\mathbf{r}(x) = 
(\begin{bmatrix}
1\\2
\end{bmatrix}x+
\begin{bmatrix}
3\\4
\end{bmatrix})(
\begin{bmatrix}
2 \\ 3
\end{bmatrix}x + 
\begin{bmatrix}
7\\2
\end{bmatrix}
)=$$
$$
=\begin{bmatrix}
2\\6
\end{bmatrix}x^2+
\begin{bmatrix}
7\\4
\end{bmatrix}x+
\begin{bmatrix}
6\\12
\end{bmatrix}x+
\begin{bmatrix}
21\\8
\end{bmatrix}$$
$$=
\begin{bmatrix}
2\\6
\end{bmatrix}x^2+
\begin{bmatrix}
13\\16
\end{bmatrix}x+
\begin{bmatrix}
21\\8
\end{bmatrix}
$$

When we multiply each of the vectors together, we take the Hadamard product (element-wise product, denoted with $\circ$).

Note that if we plug $x = 2$ into the resulting vector polynomial, we get the following:

$$
\begin{bmatrix}
2\\6
\end{bmatrix}(2)^2+
\begin{bmatrix}
13\\16
\end{bmatrix}(2)+
\begin{bmatrix}
21\\8
\end{bmatrix}=
\begin{bmatrix}
55\\64
\end{bmatrix}
$$

This is the same as if we compute:

$\mathbf{l}(2)\circ\mathbf{r}(2) = \begin{bmatrix}5\\8\end{bmatrix}\circ\begin{bmatrix}11\\8\end{bmatrix}=\begin{bmatrix}55\\64\end{bmatrix}$

- Source MD : https://github.com/RareSkills/zk-book/blob/prod/content/r1cs-zkp/en/r1cs-zkp.md

### Verification step
Thus, the verification step becomes

$$

\left[ \begin{array}{c}
\sum_{i=1}^m l_{i,1}[a_i G_1]_1 \\
\sum_{i=1}^m l_{i,1}[a_i G_1]_1 \\
\vdots \\
\sum_{i=1}^m l_{i,1}[a_i G_1]_1
\end{array} \right]
\begin{matrix}
\bullet \\
\bullet \\
\vdots \\
\bullet
\end{matrix}
\left[ \begin{array}{c}
\sum_{i=1}^m r_{i,1}[a_i G_2]_2 \\
\sum_{i=1}^m r_{i,1}[a_i G_2]_2 \\
\vdots \\
\sum_{i=1}^m r_{i,1}[a_i G_2]_2
\end{array} \right]

\stackrel{?}{=}
\left[ \begin{array}{c}
\sum_{i=1}^m o_{i,1}[a_i G_1]_1 \\
\sum_{i=1}^m o_{i,1}[a_i G_1]_1 \\
\vdots \\
\sum_{i=1}^m o_{i,1}[a_i G_1]_1
\end{array} \right]
\begin{matrix}
\bullet \\
\bullet \\
\vdots \\
\bullet
\end{matrix}
\left[ \begin{array}{c}
G_2 \\
G_2 \\
\vdots \\
G_2
\end{array} \right]
$$

$$
=
\begin{array}{c}
 \sum_{i=1}^m l_{i,1}[a_i G_1]_1\bullet \sum_{i=1}^m r_{i,1}[a_i G_2]_2 \\
 \sum_{i=1}^m l_{i,2}[a_i G_1]_1\bullet \sum_{i=1}^m r_{i,2}[a_i G_2]_2  \\
\vdots \\
\sum_{i=1}^m l_{i,n}[a_i G_1]_1\bullet \sum_{i=1}^m r_{i,n}[a_i G_2]_2
\end{array}
\stackrel{?}{=}
\begin{array}{c}
\sum_{i=1}^m o_{i,1}[a_i G_1]_1\bullet G_2 \\
\sum_{i=1}^m o_{i,2}[a_i G_1]_1\bullet G_2 \\
\vdots \\
\sum_{i=1}^m o_{i,n}[a_i G_1]_1 \bullet G_2
\end{array}
$$

The above vectors of $G₁₂$ elements will be element-wise equal if and only if the prover has provided a valid witness.

Well, almost. We’ll get to that in a following section.
 
First we need to mention an important implementation detail


# Sample test form Chat GPT

# Heading Level 1
## Heading Level 2
### Heading Level 3
#### Heading Level 4
##### Heading Level 5
###### Heading Level 6

**Teks Tebal**  
*Italic (Miring)*  
~~Strikethrough (Coretan)~~  
**_Bold dan Italic (Tebal dan Miring)_**

> Ini adalah contoh kutipan.
>> Kutipan bertingkat.

1. Item pertama
2. Item kedua
   1. Sub-item pertama
   2. Sub-item kedua
3. Item ketiga

- Item pertama
- Item kedua
  - Sub-item pertama
  - Sub-item kedua
- Item ketiga

[Contoh Tautan](https://example.com)

![Contoh Gambar](https://via.placeholder.com/150)

Contoh `inline code`.

\```python
def hello_world():
    print("Hello, World!")
\```

| Header 1 | Header 2 | Header 3 |
|----------|----------|----------|
| Row 1    | Data 1   | Data 2   |
| Row 2    | Data 3   | Data 4   |

---

- [x] Selesai
- [ ] Belum selesai

:smile: :+1: :heart:

Ini adalah contoh teks dengan catatan kaki [^1].

[^1]: Ini adalah catatan kaki.

Istilah 1  
: Definisi 1

Istilah 2  
: Definisi 2

- [ ] Task 1
- [x] Task 2 (Selesai)
- [ ] Task 3



