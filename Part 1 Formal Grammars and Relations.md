# What is a Formal Grammar?
## Defining formal grammars
- We have our alphabet $Σ$, the elements of which we call terminal symbols (and often use $\{a, b, c, . . .\}$). 
- We have a disjoint set of symbols $N$ , the elements of which we call non-terminal symbols (and often use capital letters). $\{S,T,X,V,W\}$ 
- There is a special start symbol $S ∈ Γ$. 
- $\Sigma ^*$ refers to the set of all possible strings that can be made with the alphabet
- $(\Sigma \cup \mathcal{N})^*$ refers to the set of all possible words that can be made
- A grammar then is a finite list of pairs $(u, w)$ with $u, w ∈ (Σ ∪ N )^ ∗$ (called production rules, and often written $u → w$).

**A simple grammar example**
Let $Σ = \{a, b\}, N = \{S, T \}$ and the production rules be  
- $S →ε$ 
- $S →aT$
- $T →bS$  
The resulting language is:  
$${(ab)^n |n ∈ \mathbb{N}}= \{ε, ab, abab, ababab, . . .\}$$
$\epsilon$  is the empty word

## How a formal grammar defines a language
#### Definition 
A grammar $G$ defines a language $L(G) ⊆ Σ^ ∗$ by saying that $t ∈ L(G)$ if we can reach $t$ with the following process: 
1. Start with S. 
2. Write our current word as $v_0uv_1$, and pick a rule $(u, w)$. Then replace the current word by $v_0wv_1$. 
3. If the current word is $t$, stop, else repeat Step 2.

#### Example 
Let $Σ = \{a, b\}, N = \{S\}$ and the rules be $S → ε, S → aSa$ and $S → bSb$. 
- This grammar defines the even-length palindroms over $\{a, b\}$.

## A “real” grammar 
#### Example 
Let $Σ = \{\text{the, dog, cat, eats, sleeps}\},$ $$N = \{\text{S, NOUN, NP, VP, TRANS-VERB, INTRANS-VERB}\}$$ and the rules be S → NP VP, NP → the NOUN, NOUN → cat, NOUN → dog, VP → INTRANS-VERB, VP → TRANS-VERB NP, TRANS-VERB → eats, INTRANS-VERB → sleeps, INTRANS-VERB → eats. 
###### Task 
Find all “words” (ie sentences) belonging to the language of this grammar.

#### A complicated grammar example
Let $Σ = \{a, b, c\}, N = \{S, T , X , Y \}$ and the production rules be  
- $S →Tabc$
- $T →ε$
-  $T →TXY$ 
- $XYa →aXY$
- $Yb →bY$
- $aXb →aab$
- $bYc →bbcc$  
This describes the language:  
$$\{a^n b^n c^n |n ≥1\}= \{abc, aabbcc, aaabbbccc, . . .\}$$

#### Outlook 
- Without restrictions on how rules might look like, it can be very time consuming to show that a word belongs to the language, 
- and impossible(!!) to show that a word does not. 
- We can formalize the derivation process a bit more, by introducing the transitive closure of a relation.
###### List of topics
- Formal Grammar definition

###### Links
- [introduction to formal grammars](https://youtu.be/U-rg4nHeYiw) 

# The Chomsky hierarchy
## The hierarchy, overview 
From simplest to most complicated: 
3. Regular languages (having right-linear grammars) 
2. Context-free languages (having context-free grammars) 
1. Context-sensitive languages (having context-sensitive grammars) 
0. Computably enumerable languages (having (unrestricted) grammars) 
-1.  Arbitrary languages (not necessarily describable by a grammar at all)

## Right-linear grammars
**Definition** 
A grammar is *right-linear*, if all rules are of the form $T → ε$ or $T → aR$ for $T, R ∈ N$ and $a ∈ Σ$. I.e. the right hand side ends with non-terminal letters. We shall also allow the form $T → a$ as abbreviation for $T → aQ, Q → ε$ for a fresh non-terminal $Q$. 
**Definition** 
A grammar is *left-linear*, if all rules are of the form $T → ε$ or $T → Ra$ for $T, R ∈ N$ and $j$. I.e. the right hand side starts with non-terminal letters
**Theorem** 
*Right-linear* and *left-linear* grammars describe the same languages.

## Context-free grammars 
#### Definition 
A grammar is *context-free*, if the left-hand side of every rule is a single non-terminal.

Let $Σ = \{a, b, c\}, N = \{S, T , X , Y \}$ and the production rules be  
- $S →Tabc$
- $S \rightarrow SA$
- $A \rightarrow bSc$
- $A \rightarrow ba$
- $T →ε$
- $T →TXY$ 
- $X \rightarrow XYab$

## Context-sensitive grammars
#### Definition 
A grammar is *context-sensitive*, if every rule is of the form $wAu → wvu$ where $v \neq ε$; or is $S → ε$, and where $S$ never appears on the right-hand side of a rule. 
Let $\Sigma = \{a,b,c\}$ and $N = \{A,B\}$

- $S → abc$
- $S \rightarrow aAbc$
- $Ab → bA$
- $Ac → Bbcc$
- $bB → Bb$
- $aB → aa$
- $aB \rightarrow aaA$
- $bB \rightarrow \epsilon$
#### Definition
A grammar is monotonic, if for all rules $u → w$ (except potentially $S → ε$) it holds that $|u| ≤ |w|,$ ($|\cdot|$ being length) and $S$ never appears on the right-hand side of a rule. 
#### Theorem
A context sensitive grammar is monotonic
Every context-sensitve grammar is monotonic, or
[or for every monotonic grammar there is an equivalent context-sensitive grammar](https://cs.stackexchange.com/questions/7734/demonstrating-that-for-every-monotonic-grammar-there-is-an-equivalent-context-se)
(link to proof)

###### Links


# Relations and transitive closure
## Relations 
#### Definition 
A relation between sets $X,Y$ is a subset $R ⊆ X × Y$. A relation on $X$ is a subset $R ⊆ X × X.$
#### Properties of relations
**Reflexive** if $∀a ∈ X (a, a) ∈ R$
**Symmetric** if $∀a, b ∈ X (a, b) ∈ R ⇒ (b, a) ∈ R$ 
**Anti-reflexive** if $∀a ∈ X (a, a) \notin R$
**Anti-symmetric** if $∀a, b ∈ X ((a, b) ∈ R ∧ (b, a) ∈ R) ⇒ a = b$ 
**Total** if $∀a, b ∈ X (a, b) ∈ R ∨ (b, a) ∈ R$
**Transitive** if $∀a, b, c ∈ X ((a, b) ∈ R ∧ (b, c) ∈ R) ⇒ (a, c) ∈ R$

**Example** 
Let $R ⊆ \{0, 1, 2, 3\} × \{0, 1, 2, 3\}$ be defined as $R = \{(0, 1),(2, 3)\}$. Which properties does $R$ have? 

**Example** 
Let $| ⊆ \mathbb{N} × \mathbb{N}$ be defined as $(n, m) ∈ |$ iff $n$ divides $m$. Which properties does $|$ have?

#### Definitions
A ***linear order*** is a  anti-symmetric, total and transitive relation. 
An ***equivalence relation*** is a reflexive, symmetric and transitive relation.

## Composition of relations
#### Definition 
Given $R ⊆ X × Y$ and $Q ⊆ Y × Z$, let $(Q ◦ R) ⊆ X × Z$ be defined as : $$(Q ◦ R ) = {(x, z) ∈ X × Z | ∃y ∈ Y (x, y) ∈ R ∧ (y, z) ∈ Q}$$
## Transitive closure
#### Definition 
Let $R$ be a relation on $X$. We define $R^1 := R$, and $R^{n+1} := R^n ◦ R$, and then $R^+ = \cup_{n≥1}R^n.$ 

The transitive closure is a mathematical operation that extends a binary relation between elements of a set to include all pairs of elements that are related by a path of one or more intermediate elements.

Formally, given a binary relation $R$ on a set $S$, the transitive closure of $R$, denoted by $R^+$, is defined as the smallest transitive relation that contains $R$. In other words, $R^+$ includes all pairs $(a, b)$ such that there exists a sequence of elements $a = x_1, x_2, ..., x_n = b$ in $S$, such that $(x_i, x_{i+1})$ is in $R$ for all $1 \leq i < n$.

In other words, $R^+$ contains all the pairs of elements in $A$ that can be related to each other by a finite sequence of steps using $R$. For example, if $R$ represents the parent-child relationship in a family tree, then the transitive closure $R^+$ would include all the pairs of elements that are related as grandparents-grandchildren, great-grandparents-great-grandchildren, and so on.

Intuitively, we can think of the transitive closure as the "closure" of the relation $R$ under the transitive property. That is, if $R$ relates $a$ to $b$, and $b$ to $c$, then $R^+$ includes the pair $(a,c)$ as well. In other words, the transitive closure adds all the pairs of elements that are related through a sequence of intermediate steps in $R$.


#### Theorem 
The relation $R^+$ is the smallest transitive relation extending $R$, and we thus call it the transitive closure of $R$. 
#### Example 
Let $S = \{(n, n + 1) | n ∈ \mathbb{N}\}$. Then $S^+ = <$.

# The derivation relation
#### Definition 
Consider a grammar $G$ specified by terminals $\Sigma$, non-terminals $\mathcal{N}$ , start symbol $S$ and set rules $R$. The one-step derivation relation on $(Σ ∪ \mathcal{N} )^∗$ is defined as: $$\hookrightarrow := \{(\text{uvw, uv′w}) | u, v, w, v ′ ∈ (Σ ∪ \mathcal{N} )^∗ \quad (v, v′) ∈ R\}$$
**Explanation**
In the context of formal languages and automata theory, the one-step derivation relation is a binary relation between strings, denoted by the symbol $\hookrightarrow$. It represents the ability of a formal grammar to generate a string by replacing a single nonterminal symbol with a string of terminal and/or nonterminal symbols.

More formally, given a context-free grammar $G = (V, Σ, R, S)$, where $V$ is a set of nonterminal symbols, $Σ$ is a set of terminal symbols, $R$ is a set of production rules, and $S$ is the start symbol, the one-step derivation relation is defined as follows:

For any strings $α, β$, and $γ \in (V ∪ Σ)*$ and any nonterminal symbol $A ∈ V, αAβ → αγβ$ if and only if there exists a production rule $A → γ \in R$.

This means that if the nonterminal symbol $A$ appears in the middle of a string $αAβ$, it can be replaced with the string $γ$ to obtain a new string $αγβ$. This new string can then be used as input to the one-step derivation relation again, possibly leading to further string expansions.

The one-step derivation relation is an important concept in the theory of formal languages, since it provides a way to formally define the notion of a context-free grammar generating a language. By repeatedly applying the one-step derivation relation, it is possible to generate all the strings in the language generated by a context-free grammar.

#### Definition 
The derivation relation $$ \hookrightarrow\mathrel{\mspace{-15mu}}\rightarrow :=\hookrightarrow ^+$$ is defined as the transitive closure of the one-step derivation relation.

## Infix notation
We typically use infix notation for the (one-step) derivation relation, i.e. we write $u \hookrightarrow w$ for $(u, w) ∈ \hookrightarrow$ and $u ,\hookrightarrow\mathrel{\mspace{-15mu}}\rightarrow w$ for $(u, w) ∈ ,\hookrightarrow\mathrel{\mspace{-15mu}}\rightarrow$. 
(Just as we write $n|m$ for $n$ divides $m$, and $x = y$ rather than $(x, y) ∈ =, etc.)$.

# The language defined by a grammar
#### Definition 
The language defined by a grammar $G$ is: $$L(G) := \{w ∈ Σ^∗ | S \hookrightarrow\mathrel{\mspace{-15mu}}\rightarrow w\}$$
A grammar is a formal system that specifies a language in terms of its rules for generating strings in that language. A grammar consists of a set of nonterminal symbols, a set of terminal symbols, a start symbol, and a set of production rules.

The language defined by a grammar $G$ is the set of all strings that can be generated by the grammar. This is denoted by $L(G)$ and is defined as follows:
$$L(G) := \{w \in \Sigma^* \mid S \hookrightarrow\mathrel{\mspace{-15mu}}\rightarrow w\}$$
where $\Sigma$ is the set of terminal symbols, $S$ is the start symbol, and the relation $\hookrightarrow\mathrel{\mspace{-15mu}}\rightarrow$ denotes a sequence of productions that can be used to generate a string from the start symbol. In other words, $L(G)$ consists of all strings that can be derived from the start symbol $S$ by applying a sequence of production rules.

To summarize, the definition of $L(G)$ in automata theory specifies the language generated by a grammar $G$, which is the set of all strings that can be derived from the start symbol $S$ by applying a sequence of production rules.