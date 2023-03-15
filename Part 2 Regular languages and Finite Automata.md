# Non-deterministic finite automata: Definition
**Definition**
A non-deterministic finite automaton over an alphabet $Σ$ is  given by a set $V$ of states, a transition relation $δ ⊆V ×Σ ×V$, a  start state $s ∈V$ and a set of accepting (or final) states $F ⊆V$.

**A finite state automaton 1**
![[Pasted image 20230314152250.png]]
### A run of an automaton  
**Definition**
A run of an automaton $\mathcal{A}$ on a word $w ∈Σ^∗$ is a word  $q_0q_1 ...q_{|w|} ∈V^∗$ such that $q_0 = s$ and  $∀i < |w|(q_i,w_i,q_{i+1}) ∈δ$. If $q_{|w|} ∈F$, it is *accepting*, otherwise it is rejecting. An automaton accepts a word $w ∈Σ^∗ \iff \exists$ an accepting run on $w$. We let $L(A)$ be the language of  all words accepted by $\mathcal{A}$.

![[Pasted image 20230314153012.png]]
$abba ⇒$ no  
$baaba ⇒$ yes

## Reversal of a language
**Definition**
Given a word $w ∈Σ^∗$, let its reversal $w^R∈Σ^∗$ be defined by  $|w^R|= w$ and $w^R(i) = w(|w|−i −1)$.  
(This literally says that $w^R$ is w read backwards.)

**Definition**  
Given a language $L ⊆Σ^∗$, let $L^R:= {w^R|w ∈L}$.
**Theorem**  
If $L$ is regular, then so is $L^R$.

**Outlook**  
- Deterministic automata would be even nicer.  
- Regular languages are closed under union, intersection, interleaving.  
- Regular expressions!

# Non-deterministic finite automata and  Regular Languages
**Definition**  
A non-deterministic finite automaton over an alphabet $Σ$ is given by a set $V$ of states, a transition relation $δ ⊆V ×Σ ×V$, a start state $s ∈V$ and a set of accepting (or final) states $F ⊆V$.
![[Pasted image 20230314153012.png]]
**Equivalence**  
**Theorem**  
Right-linear grammars and non-deterministic automata describe the same languages. (We call those languages regular.)
**Theorem**  
Right-linear grammars and non-deterministic automata  describe the same languages. (We call those languages regular.)
*Proof.*  
We translate back and forth:  
- Non-terminal symbols correspond to states (start symbol to start state).  
- We have a rule $T →ε \iff$ the state T is final.  
- We have a rule $T →aR \iff$ there is a transition  $(T,a,R) ∈δ$.

**Exercise**
Take the grammar with non-terminals $\mathcal{N} = {S,A,B,C}$ and rules $$S →ε, S →aA, S →bB, S →aC, A →aA, A →bB,B →aC, B →bC, C →ε, C →aA.$$
Draw the automaton it corresponds to.

 # From non-deterministic to determinsitic
### Non-deterministic vs deterministic finite automata  
**Definition**  
A non-deterministic finite automaton over an alphabet $Σ$ is given by a set $V$ of states, a transition relation $δ ⊆V ×Σ ×V$ , a  start state $s ∈V$ and a set of accepting (or final) states $F ⊆V$.  
**Definition**  
A deterministic finite automaton over an alphabet $Σ$ is given by a set $V$ of states, a transition function $δ : V ×Σ →V$ , a start state $s ∈V$ and a set of accepting (or final) states $F ⊆V$.
*A Technicality*
A state in a deterministic finite automaton has outgoing edges with all labels – but we usually don’t draw dead ends.
*Equivalence*  
**Theorem**  
Deterministic and non-deterministic finite automata recognize the same languages.

#### The powerset construction
**Definition**  
By $P(X)$ we denote the powerset of the set $X$, i.e. $P(X) = {S |S ⊆X}$.  
**Proof.**  
Given a non-deterministic finite automaton with states $V$ and transition relation $δ$, let the powerset construction automaton be the deterministic finite automaton with:  
- states $P(X)$
- transition function $∆$ where $∆(S,a) = {q ∈V |∃r ∈S (r ,a,q) ∈δ}$
- initial state ${s}$ (where $s$ is the initial state of the original automaton)  
- final states ${S |S ∩F \neq ∅}$(where $F$ is the set of final states of the original automaton)
###### A consequence  
**Definition**  
Given a language $L$, let $L^C = {w ∈Σ^∗ |w \notin L}$.  
**Corollary**  
If $L$ is regular, then so is $L^C$ .

###### A heads-up  
- Determinizing a non-determinsitic finite automaton is a very natural exam question.  
- Prractise it!  
- Check your answers by trying out a few words to see whether both automata give the same answer.

# Closure properties of regular languages
Recap  
We are exploring the class of regular languages. Those are  described by:  
1. Right-linear grammars (definition)  
2. Left-linear grammars (theorem)  
3. Non-deterministic finite automata (theorem)  
4. Deterministic finite automata (theorem)  
If $L$ is a regular language, then so is $L^R$ (its reversal).

##### A closure property  
**Theorem**  
If $L_1,L_2$ are regular languages, then so are $L_1 ∩L_2$ and $L_1 ∪L_2$.

##### The technical tool
**Definition**  
Given two finite automata $\mathcal{A}_i = (V_i,s_i,δ_i,F_i)_{i∈\{1,2\}},$ let their product be $(V_1 ×V_2,(s_1,s_2),δ×,F)$ where  
1. $((q_1,q_2),a,(q′_1,q′_2)) ∈δ_×  \iff (q_i,a,q′_i ) ∈δ_i$ for both $i ∈\{1,2\}$ (non-deterministic case)  
2. $δ_×((q_1,q_2),a) = (δ_1(q_1,a),δ_2(q_2,a))$ (deterministic case)  
3. and $F = F_1 ×F_2 = \{(q_1,q_2) |q_1 ∈F_1 ∧q_2 ∈F_2\}$  
The product automaton recognizes the intersection of the languages recognized by its constituents.

**Argument for union**  
1. We are given two grammars $G_1$ and $G_2$.  
2. We add a “fresh copy” $S'′$ of the start symbol to each grammar, and for any rule with $S$ on the left add the corresponding version with $S′$ instead, and replace any $S$ on the right with $S′$.  
3. Rename all non-terminals in $G_2$ to be distinct of those in $G_1$.  
4. Gather all rules together, and we have a formal grammar for $L(G_1) ∪L(G_2)$.
##### Complement  
**Theorem**  
If $L$ is a regular language, so is $Σ^∗ \backslash L$ (meaning all words not  belonging to $L$).  
**Proof.**  
Take a deterministic automaton for L (including dead ends!!!),  and make final states non-final and non-final states final. $\square$

###### Concatenation  
**Definition**  
Given languages $L_1, L_2$, let their concatenation be  $L_1 ◦L_2 := {uw |u ∈L_1 ∧w ∈L_2}$ 
(sometimes written at $L_1L_2$).  
**Theorem**  
If $L_1,L_2$ are regular, then so is $L_1 ◦L_2$.
##### Concatenation, proof via grammars
**Proof.** 
- Let $L_1 = L(G_1), L_2 = L(G_2)$ with right-linear $G_1,G_2$ (no $T →a$-type rules).  
- Rename all non-terminals in $G_2$ to be disjoint from those in $G_1$, with $S_2$ being the new start symbol.
- Change any rule of the form $T →ε$ in $G_1$ to be $T →S_2$ instead. 
- Put everything in one grammar $G$, we have that  $L(G) = G_1 ◦G_2$.

##### Kleene-star  
**Definition**  
Given a language $L$, let $L^0 = {ε}$, $L^{n+1} = LL^n$ and $L^∗ = \cup_{n∈\mathbb{N}}L^n$.  
**Theorem**  
If $L$ is regular, so is $L^∗$.

###### Summary
**Regular languages**  
**Definition**  
We call a formal language regular, if there exists a right-linear  
grammar describing it.  
**Theorem**  
The following are equivalent for a formal language:  
1. It is regular.  
2. There exists a left-linear grammar describing it.  
3. There exists a non-deterministic finite automaton describing it.  
4. There exists a deterministic finite automaton describing it.  
5. There exists a regular expression describing it.

**Closure properties**  
**Theorem**  
If $L_1$ and $L_2$ are regular languages, then so are:  
1. L^R_1  
2. L_1 ∩L_2  
3. L_1 ∪L_2  
4. $Σ^∗\backslash L_1$  
5. $L_1 ◦L_2$  
6. $L^∗_1$

###### Excercises
1. Find a left-linear grammar for the language $\{aab,bbbb\}$.  
2. Try to construct a finite automaton for the language over the alphabet $Σ = {a,b}$ of all words with exactly 3 b’s in it.  
3. Try to construct a finite automaton for $\{a^nb^m |n,m ∈\mathbb{N}\}$.  
4. Try to construct a finite automaton for ${a^nb^n |n ∈\mathbb{N}}$.
# Closure properties and regular expressions

**Meaning**  
1. $∅$ denotes the empty language.  
2. $ε$ denotes the language $\{ε\}$  
3. a denotes the language $\{a\}$  
4. $R|Q$ denotes the language given by the union of the languages denoted by $R,Q$  
5. $RQ$ denotes the language given by the concatenation of  the languages denoted by $R,Q$  
6. $R^∗$ denotes the language given by the Kleene star of the language denoted by $R$

###### Connection  
**Theorem**  
A language is regular if and only if there is a regular expression denoted by it.  
- That regular expressions denote regular languages follows from the closure properties we saw today.  
- We’ll leave the other direction for later.

# The pumping lemma
*Motivating example*  
We had seen the grammar  
- $S →aTb$
- $T →ε$  
- $T →TXY$  
- $YX →XY$  
- $aX →aa$  
- $Yb →bb$  
describing the language $\{a^nb^n |n > 0\}$.

The context-free grammar  
- $S →aSb$
- S →ab  
describes the same language $\{a^nb^n |n > 0\}$ much more elegantly.

###### The pumping lemma  
If $L$ is regular, then $∃k ∈\mathbb{N}$ such that $∀p ∈L, |p|≥k$ there exists ($∃$) a splitting $p =uvw$ where $|uv|≤k$ and $v \neq \epsilon$ such that  $∀_i ∈ \mathbb{N}$ it holds that $uv^iw ∈L$.

###### Pumping lemma, contraposition  
- If for all $k ∈\mathbb{N}$ you can pick a word $p ∈L$ with $|p|≥k$
- such that however $p$ is written as $p =uvw$ (subject to $|uv|≤k$ and $v \neq ε$)  
- you can find some $i ∈ \mathbb{N}$ such that $uv^iw \notin L$, 
- then $L$ is not regular.

**An application**  
**Question**  
Is $L_{pal} =\{u ∈\{a, b\}^∗|u =u^R\}$ regular?  
- We get some $k ∈\mathbb{N}$.  
- We pick $a^kba^k ∈ L_{pal}$.  
- If $uvw =a^kba^k, |uv|≤k$ and $v \neq \epsilon$, then $v =a'$ for some $1 ≤l ≤k$. So $uv^2w =a^{k+l}ba^k \notin L_{pal}$.  
**Proposition**  
$L_{pal}$ is not regular.

Task: Prove that ${a^nb^n |n ∈\mathbb{N}}$ is not regular.

##### Pumping lemma, contraposition  
- If for all $k ∈\mathbb{N}$ you can pick a word $p ∈L$ with $|p|≥k$
- such that however $p$ is written as $p = uvw$ (subject to  $|uv |≤k$ and $v \neq ε$)  
- you can find some $i ∈ \mathbb{N}$ such that $uv^i w \notin L$,  
- then $L$ is not regular.
**An application**  
Consider the language over the alphabet $Σ = {(, ), +, ×, 0, 1, 2}$  generated by the following grammar:  
- $S →0 ; S →1 ; S →2$
- $S →(S + S)$
- $S →(S ×S)$  
**Question**  
Is there a finite automaton recognizing it?

**Pumping lemma says no**  
- We are given $k ∈\mathbb{N}$  
- We pick $(((..(0 + 0) + 0) + ...+) = (^k0[+0)]^k$ as the word from our language.  
- Any decomposition $(^k0[+0)]^k = uvw$ with $|uv |≤k , v \neq ε$  means that $v = (^{\mathscr{L}}$ for some $\mathscr{L} > 0)$.  
- Now $uv^2w = (^{k +\mathcal{L}}0[+0)]^k$ has an imbalance of left and right parenthesis, and thus does not belong to our language.  
- By the pumping lemma, the language is not regular.
###### Another example  
**Question**  
Let $L_{\mod 3}$ = $\{a^n |n \mod 3 = 0\}$. Is $L_{\mod 3}$ regular?  
Yes, it is (built an automaton with 3 states).

**Question**  
Let $L_p = \{a^n |n \text{ is prime}\}$. Is $L_p$ regular?  
- We are given $k ∈\mathbb{N}.$
- Let $j > k + 1$ be a prime number. Our word is $a^j ∈L_p$ .
- Consider any decomposition $a^j = uvw$ with $|uv|≤k$ and  $v \neq ε$. 
- Then $v = a^{\mathscr{L}}$ and $uw = a^{j −\mathscr{L}}$ with $\mathscr{L} > 0$ and $j − \mathscr{L} > 1$. For any $i ∈ \mathbb{N}$, $uv ^i w = a^{i\mathscr{L}+j −\mathscr{L}}$. So  $uv ^{j − \mathscr{L}}w = a^{\mathscr{L}(j −\mathscr{L})+j −\mathscr{L}}$= $a^{(\mathscr{L}+1)(j −\mathscr{L}}$). But $(\mathscr{L} + 1)(j −\mathscr{L})$ is not  prime, so this word does not belong to our language.