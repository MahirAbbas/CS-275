# What is a Formal Language?
## **Words over an alphabet** 
#### Definition (Words of fixed length) 
Let $Σ$ be a (finite) set (which we will call the alphabet) and $n ∈ N$ a natural number. With $Σ$ n we denote the set of functions from $\{0, 1, . . . , n − 1\}$ to $Σ$, also called words of length $n$. 
#### Example 
Let $Σ = \{a, b\}$. Then $Σ^ 3 = \{aaa, aab, aba, abb, baa, bab, bba, bbb\}$, where e.g. $aba$ denotes the function returning a for inputs $0$ and $2$, and $b$ for input 1.
#### Remarks 
- Calling Σ an alphabet is expressing what we use $Σ$ for, it is not constraining what kind of set $Σ$ could be. 
- We treat elements of $Σ$ as atomic. If $Σ = \{10\}$, then $Σ^ 2 = \{(10)(10)\}$. If $Σ = {0, 1}$, then $101 ∈ Σ ^3$ denotes the string “101”, not the numbers 101 or 9. 
- While $Σ$ and $Σ^ 1$ are formally distinct things, we can often identify them (like implicit type casting in programming). 
- Regardless of $Σ$, there is a single element in $Σ^ 0$ , the empty word $ε$.

## Formal languages 
#### Definition 
Let $Σ^ ∗ = \cup_{n∈ \mathbb{N}}Σ^ n$ be the union of the set of words of all lengths over $Σ$. 
#### Definition 
For $w ∈ Σ ^∗$ , we write $|w| = n$ to express that $w ∈ Σ^ n$ . 
#### Definition 
A (formal) language over the alphabet $Σ$ is a subset $L$ of $Σ^ ∗$

## Examples of formal languages 
- Let $Σ$ be the set of ASCII-characters, and $L$ the set of valid Java programs. 
- Let $Σ$ be the set of ASCII-characters, and $L$ the set of valid Java programs that don’t erase the disk. 
- Let $Σ$ be the words listed in the Oxford dictionary, and $L$ be the set of grammatically correct English sentences using these words. 
- Let $Σ = \{0, 1\}$, and $L$ be the set of binary encodings for graphs having a Hamiltonian cycle.

## Composition 
#### Definition 
We define the composition of words $◦ : Σ^∗ × Σ ^∗ → Σ^ ∗$ via $|w ◦ u| = |w| + |u|, (w ◦ u)(i) = w(i)$ if $i < |w|$, and $(w ◦ u)(i) = u(i − |w|)$ else. 
- It holds that $(u ◦ v) ◦ w = u ◦ (v ◦ w)$. 
- $ε ◦ u = u ◦ ε = u$. 
- We usually drop the $◦$, and just write e.g. $uvw$ for $(u ◦ v) ◦ w$.

