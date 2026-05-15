# Development Log – The Torchbearer

**Student Name:** __________Adam Mohamed_________________
**Student ID:** ___________133870929________________

---

## Entry 1 – [Date]: May 9th, 2026 - Initial Plan


_After reading the instructions and requirenments, the things I do plan to implement first would be doing the functions in order but trying to finish Dijkstra and find optimal route, as Dijkstra's is meant to help with computing the shortest between any S and T, and for find optimal route I plan to tackle this ASAP as this one will definitly be a bit more convuluted and need more time debugging and fixing wrong assumptions. I plan to test with a lot of print statement and leverging the temp test information.  _

---

## Entry 2 – [Date]: May 11th: 2026 [Short description]

_On this day after finishing part two, i realized i was solving the question as if it was setup to where an array is all we needed to map the nodes, since im used to seeing graph nodes set up in a way where we can doo arr[node] for any value and it'll show the optimal path for that ndoe at that index. I resolved once I realized the keys are able to be strings and I looked more at the bottom screen test cases and it helped solve the trifecta of source_nodes -> dijkstra -> precompute distances. One other issue I ran into was python issues and forgetting iterating a map doesn't actually release key,value pairs like a [node,(v,u)] would do in a normal iteration._

---

## Entry 3 – [Date]: May 14th: 2026 [Short description]

_On this day, It was easily the most difficult and time consuming part of the implementation. To start, understanding the implementation of solving the find_optimal_path, and noting the fact i immplemented a variable as a set rather than a list and was getting a constant"pop from an empty set" error code after completeting solve(). Thats just part one of the issues. Next, I tried to implement the base case around T, forgetting the entrie premise of the problem of we need every relic before we move to finding T. The logic was semi there, you do figure out the cost from the last relic to T, but you need to do it after you emptied the relics array. One last note on errors, it was a pain for almost 30 minutes of debugging trying to figure out why my minimum path had neither the correct optimal cost and the ordered array was empty. The reason was the logic python uses for assignments is similar to javascripts and I never noticed that. Setting best as (cost_so_far, relics_ordered) WOULD ADD THE CONSISTENT VALUES TO THE MEMORY ADDRESS LISTED. Im far to used to how c++ does this logically with assignments, and far to blind to know python did this without me realizing because my print statments were showing the builds._

---

## Entry 4 – [Date]: May 14th:  Post-Implementation Reflection


_If I were to change anything it would probably be me wishing I could do this in another language. But on a more serious note, I do think I could've improved a bit on the logical thinking. It took me awhile before I got all test cases passed because I kept overlooking slight details. _

---

## Final Entry – [Date]: Time Estimate

| Part | Estimated Hours |
|---|---|
| Part 1: Problem Analysis | 30m |
| Part 2: Precomputation Design | ~ 1hr 40m |
| Part 3: Algorithm Correctness | ~ 33m |
| Part 4: Search Design | ~ 40 |
| Part 5: State and Search Space | find_optimal_path() + _explore() = ~2hr: 45m |
| Part 6: Pruning | ~30m |
| Part 7: Implementation | Code Implementation + debugging? : ~6hrs | 
| README and DEVLOG writing | ~2hr |
| **Total** | Part 7 is an accumlation estimate for code total:, not counting it: ~9h with debugging |
