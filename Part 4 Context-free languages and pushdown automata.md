# Context-free languages
###### A context-free language which is not regular  
**Proposition**  
The language $\{a^nb^n |n ∈\mathbb{N}\}$ is context-free, but not regular.

###### Parse trees  
**Definition**  
A parse tree for a context-free grammar is a tree labelled by terminals, non-terminals and $ε$ subject to the following rules:
1. The root is labeled $S$.
2. A vertex is a leaf iff it is labeled by a terminal or $ε$.
3. For every non-leaf $v$ there is a rule with the label of $v$ on the left, and the concatenation of the child labels on the right.
**Theorem**
The language generated by a context-free grammar consists exactly of the words built from the terminals on the leaves of finite parse trees, in order.
**Parse trees**  
To show that a word belongs to the language of a context-free grammar, try to construct a parse tree bottom-up.

**Closure properties**  
**Theorem**  
Context free languages are closed under  
1. Union  
2. Concatenation  
3. Kleene-star  
4. Intersection with regular languages

##### Non-closure properties  
**Theorem**  
Context free languages are not closed under  
1. Intersection (consider $\{a^nb^nc^m |n, m ∈\mathbb{N}\}$ and  $\{a^nb^mc^m |n, m ∈\mathbb{N}\})$  
2. Complement (consider $\{uw ||u|= |w |∧u \neq w \}$)

# Pushdown automata

##### A stack  
Reminder: A stack can be implemented by a list, where we can  
only  
1. look at the first element of the list (including testing whether there is none),  
2. remove the first element of the list,  
3. and append a new element to the front of the list.

##### Pushdown automata - Informal  
- Basic idea: A pushdown automaton is a finite automaton equipped with one single stack. 
- When choosing an outgoing transition, we can take both the input symbol and the top of the stack into account.  
- Upon completing a transition, we can either push a symbol onto the stack or pop it.

###### Formal definition  
**Definition**  
A pushdown automaton over an alphabet $Σ$ is given by a tuple $(Q,Γ,δ,F)$ where  
1. $Q$ is the set of states, there is a special start state $q_0 ∈Q$, and $F ⊆Q$ is the set of final states.  
2. $Γ$ is the stack alphabet, with a special symbol $⊥ \notin Γ$ indicating that the stack is empty.  
3. $δ ⊆Q ×(Σ ∪\{ε\}) ×(Γ ∪⊥) ×Q ×(Γ ∪⊥)$ is the transition relation.

###### Configurations  
**Definition**  
1. A configuration of a pushdown automaton is an element of  $Q ×Γ^∗$.  
2. The initial configuration is $(q_0,ε)$.  
3. If the current configuration is $(q,α_0α)$, the current input symbol is a and $(q,a,α_0,q′,β) ∈δ$ for $β \notin ⊥$, then a valid subsequent configuration is $(q′,βα_0α)$.  
4. If the current configuration is $(q,ε)$, the current input symbol is a and $(q,a,⊥,q′,β) ∈δ$ for $β \notin ⊥$, then a valid subsequent configuration is $(q′,β)$.
5. If the current configuration is $(q,α_0α)$, the current input symbol is a and $(q,a,α_0,q′,⊥) ∈δ$, then a valid subsequent configuration is $(q′,α)$.
6. If the current configuration is $(q,α_0α)$ and $(q,ε,α_0,q′,β) ∈δ$ for $β \notin ⊥$, then a valid subsequent configuration is $(q′,βα_0α)$ which we can reach without progressing on the input.
7. If the current configuration is $(q,ε)$ and $(q,ε,⊥,q′,β) ∈δ$ for $β \notint ⊥$, then a valid subsequent configuration is $(q′,β)$ which we can reach without progressing on the input.
8. If the current configuration is $(q,α_0α)$ and $(q,ε,α_0,q′,⊥) ∈δ$, then a valid subsequent configuration is $(q′,α)$ which we can reach without progressing on the input.
9. The accepting configurations are $(q,⊥)$ for $q ∈F$.

##### Accepting inputs  
**Definition**  
A word is accepted by a pushdown automaton if we can reach an accepting configuration upon reading it.  
**Theorem**  
A language is recognized by a pushdown automaton iff it is generated by a context-free grammar.

**Some facts on pushdown automata**  
- The requirement that the stack needs to be emptied is not used by everyone – but we DO use it in this module.
- We could push multiple symbols on the stack at the same time.  
- If we would use a queue instead of a stack, we get something more powerful (witness $\{ww |w ∈Σ^∗\}$).
- If we had two stacks, we could recognize all computably enumerable languages.
- We don’t have an analogue to the powerset construction – we can’t require our pushdown automata to be deterministic.


# Pumping Lemma for context-free languages
**Lemma**  
If $L$ is context-free, then there is some $k ∈\mathbb{N}$ such that for every $p ∈L$ with $|p|≥k$ there is a splitting $p = uvwxy$ where $|vx|≥1$ and $|vwx|≤k$ such that for all $i ∈\mathbb{N}$ it holds that $uv^iwx^iy ∈L$.

###### Pumping Lemma for context-free languages, contraposition  
Consider a language L.  
1. If for every $k ∈\mathbb{N}$ we can chose some $p ∈L$ with $|p|≥k$,
2. such that for every splitting $p = uvwxy$ such that $|vx|≥1$ and $|vwx|≤k$,
3. we can find some $i ∈\mathbb{N}$ with $uv^iwx^iy \notin L$,
4. then $L$ is not context-free.

###### First example  
We want to show that $L = \{anbncn |n ∈\mathbb{N}\}$ is not context-free.  
1. Given the pumping length $k ∈\mathbb{N}$, we pick $a^kb^kc^k ∈L$.
2. If $a^kb^kc^k = uvwxy$ with $|vx|≥1$ and $|vwx|≤k$, we distinguish two cases:  
3. Case A: There is no $c$ in $vx$. Then $uv^0wx^0y = uwy$ has $k$-many c’s, but not also both k-many $a$’s and $b$’s. Thus, $uwy \notin L$.  
4. Case B: There is no a in vx. Then $uv^0wx^0y = uwy$ has $k$-many $a$’s, but not also both $k$-many $b$’s and $c$’s. Thus, $uwy \notin L$.  
5. Thus, L is not context-free.