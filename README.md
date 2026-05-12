# The Torchbearer

**Student Name:** _________Adam Mohamed__________________
**Student ID:** _________133870929__________________
**Course:** CS 460 – Algorithms | Spring 2026

> This README is your project documentation. Write it the way a developer would document
> their design decisions , bullet points, brief justifications, and concrete examples where
> required. You are not writing an essay. You are explaining what you built and why you built
> it that way. Delete all blockquotes like this one before submitting.

---

## Part 1: Problem Analysis

> Document why this problem is not just a shortest-path problem. Three bullet points, one
> per question. Each bullet should be 1-2 sentences max.

- **Why a single shortest-path run from S is not enough:**
  _A single shorted path run from S is not enough because a part fo the requirement of the job is to collete a set of M relics from different locations. A single short path run from S tells us the shortest path from S to T that preserving fuel, but does not consider the information of what is the optimal order to reach each relic and reach T in the shortest path / preserving fuel. _

- **What decision remains after all inter-location costs are known:**
  _The decision that remains after all inter-location costs are known is which order should we take nodes to reach all M relic chambers then T to preserve the most fuel._

- **Why this requires a search over orders (one sentence):**
  _This requires a search over orders because each permutation of relics creates a different path. Think of it as driving, to get to SDSU but you want to stop by a gas station, coffee, and breakfast, theres many roads and many routes that will reach all three but what should the order be. If the path to coffee -> breakfast -> gas -> school computes the shortest path then the GPS selects that because this permuation works the best._
---

## Part 2: Precomputation Design

### Part 2a: Source Selection

> List the source node types as a bullet list. For each, one-line reason.

| Source Node Type | Why it is a source |
|---|---|
| _Entrance to the dungeon_ | _Basic starting point to create the path from entrance to relics to T_ |
| _Dungeon/Relic chamber_ | _A dunegon, but specifically the relic chamber variation, is a source node because from a single dungeon you must know the correct path to take to the next relic chamber in order to reach t._ |

### Part 2b: Distance Storage

> Fill in the table. No prose required.

| Property | Your answer |
|---|---|
| Data structure name | Dictionary |
| What the keys represent | Dungeon/Node |
| What the values represent | Shortest Path To Node |
| Lookup time complexity | O(1) |
| Why O(1) lookup is possible | Dist[node] = The dist since the value is found immediatly |

### Part 2c: Precomputation Complexity

> State the total complexity and show the arithmetic. Two to three lines max.

- **Number of Dijkstra runs:** _Entrance + amount of relic chambers needed_
- **Cost per run:** _A single run of dijkstra is O(m log n)_
- **Total complexity:** _O(k * m log n)_
- **Justification (one line):** _K = entrance + amount of relic chambers needed, then in the same loop we do m log n for dijkstra which is O( k * m log n)_

---

## Part 3: Algorithm Correctness

> Document your understanding of why Dijkstra produces correct distances.
> Bullet points and short sentences throughout. No paragraphs.

### Part 3a: What the Invariant Means

> Two bullets: one for finalized nodes, one for non-finalized nodes.
> Do not copy the invariant text from the spec.

- **For nodes already finalized (in S):**
  _For nodes already finalized in s, its distance is already the optimal path as its proof of being in  S_

- **For nodes not yet finalized (not in S):**
  _For nodes not yet finalized, its final optimal distance is not yet known so more information is needed before a conclusion is reached for is final path._

### Part 3b: Why Each Phase Holds

> One to two bullets per phase. Maintenance must mention nonnegative edge weights.

- **Initialization : why the invariant holds before iteration 1:**
  _The invariant holds before iteration one because every node is not yet finalized thus no node is known to be the shortest path for its addition to S, only source with edge 0 and all nodes = infinity is the current state._

- **Maintenance : why finalizing the min-dist node is always correct:**
  _Finalizing the min-dist node is always correct because this means the node popped has the smallest known edge weight total from source yet,  meaning that from this point forward that node can no longer get worse from what it was finalized at._

- **Termination : what the invariant guarantees when the algorithm ends:**
  _The invariant guarantees the set of all finalized nodes is a solution for the shortest path from a source to all nodes in a graph, and anything not reachable stayed infinity from initialization._

### Part 3c: Why This Matters for the Route Planner

> One sentence connecting correct distances to correct routing decisions.

_This is imporant for route planner because you need to know the optimal/ shortets fuel path from all k source nodes needed to be able to collect every relic and exit the chamber before entering._

---

## Part 4: Search Design

### Why Greedy Fails

> State the failure mode. Then give a concrete counter-example using specific node names
> or costs (you may use the illustration example from the spec). Three to five bullets.

- **The failure mode:** _Greedy algorithm relies on hoping/selecting the local optimal choice to lead to the global optimal answer. It would not work her ebecause if we used a greedy algorithm, the selection of a relic path after x edges (counting path) could ruin the path in the later run as we would never have checked different edge weights branches. Greedy finds the minimum path its locked too, but not the actual minimum answer._
- **Counter-example setup:** _A great setup is in the assignment description since the values are already listed ( one edge change was made): S, relics: BCD, exit: T. Values are s->b 1, s->c & s->d = 2, b->c = 100, b->d = 1, b->t = 1, c->b = 1, c -> d = 100, c -> t = 100, d-> b = 1, d-> c = 1, d->t = 100. BUT THE ONE DIFFERENCE IS c->t = 100 over 1._
- **What greedy picks:** _Greedy would start at S, and select B as the connection. Then from B, It would choose the next optimal which is D, then from D -> C, straying from a recheck since B was traversed already, and C -> T for a cost of 100 is the only choice to not allow a recheck of a already checked relic chamber. Thus a path of 103 cost was formed._
- **What optimal picks:** _Optimal would choose S -> D -> C -> B -> T which is a much lwoer cost in this example (remember the difference from the test case was adding C->T = 100 for the greedy trap)._
- **Why greedy loses:** _Greedy loses horribly because of the intial trap of the minimum edge at step one led to taking a edge of 100 to finish the expedition._

### What the Algorithm Must Explore

> One bullet. Must use the word "order."

- _The algorithm must produce a valid path that creates the minimum torch fuel used, meaning we need a specific permutation or order of relics (there may be the same optimal one) that create the path from S -> T._

---

## Part 5: State and Search Space

### Part 5a: State Representation

> Document the three components of your search state as a table.
> Variable names here must match exactly what you use in torchbearer.py.

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | | | |
| Relics already collected | | | |
| Fuel cost so far | | | |

### Part 5b: Data Structure for Visited Relics

> Fill in the table.

| Property | Your answer |
|---|---|
| Data structure chosen | |
| Operation: check if relic already collected | Time complexity: |
| Operation: mark a relic as collected | Time complexity: |
| Operation: unmark a relic (backtrack) | Time complexity: |
| Why this structure fits | |

### Part 5c: Worst-Case Search Space

> Two bullets.

- **Worst-case number of orders considered:** _Your answer (in terms of k)._
- **Why:** _One-line justification._

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

> Three bullets.

- **What is tracked:** _Your answer here._
- **When it is used:** _Your answer here._
- **What it allows the algorithm to skip:** _Your answer here._

### Part 6b: Lower Bound Estimation

> Three bullets.

- **What information is available at the current state:** _Your answer here._
- **What the lower bound accounts for:** _Your answer here._
- **Why it never overestimates:** _Your answer here._

### Part 6c: Pruning Correctness

> One to two bullets. Explain why pruning is safe.

- _Your answer here._

---

## References

> Bullet list. If none beyond lecture notes, write that.

- _Your references here._
