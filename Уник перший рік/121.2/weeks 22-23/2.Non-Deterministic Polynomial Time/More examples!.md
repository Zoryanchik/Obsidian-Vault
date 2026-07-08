The traveling salesman problem (TSP) asks the following question: ‘Given a list of cities and the distances between each pair of cities, find the shortest possible route that visits each city exactly once and returns to the origin city.’

#### **(a) Decision variant of TSP:**

- _"Given a list of cities, distances, and a bound BB, does there exist a tour visiting each city exactly once and returning to the origin with total distance ≤B≤B?"_
    

#### **(b) Why are decision problems important for NP?**

- NP is defined for **decision problems** (yes/no answers). Optimization problems (e.g., "find the shortest tour") are converted to decision forms to fit the NP framework


1. What is meant by the P complexity class? Give an example of a problem in P.
- **P** is the class of **decision problems** that can be **solved in polynomial time** by a deterministic Turing machine (i.e., efficiently by an algorithm).
    
- **Example**:
    
    - **Problem**: "Is a given number nn prime?"
        
    - **Algorithm**: The AKS primality test runs in O(log⁡6n)O(log6n) time (polynomial in the number of digits).


1. What is meant by the NP complexity class? Give an example of a problem in NP.

- **NP** is the class of decision problems where a "yes" answer can be **verified in polynomial time** given a **certificate** (short proof).
    
    - Equivalently, problems solvable in polynomial time by a _nondeterministic_ Turing machine.
        
- **Example**:
    
    - **Problem**: "Does a graph GG contain a clique of size kk?" (CLIQUE problem).
        
    - **Verification**: Given a set of kk vertices, check if all pairs are connected (takes O(k2)O(k2) time).