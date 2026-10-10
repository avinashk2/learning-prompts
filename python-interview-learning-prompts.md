# Python Programming — Learning Prompts (ADVANCED, ~12h)

A complete advanced Python interview loop — coding, language, data, and design — is about 12 hours of sessions. The list below is that loop. Prompts 1–12 plus 32 cover a coding round, 13–24 plus 33 cover a language round, and 25–31 plus 34–35 cover design and the hiring conversation.

**How to use:** Open a fresh chat for each prompt below. Paste the whole code block. Work through the conversation until the LLM's end-of-session check. Move to the next prompt in a new chat.

**Coding round**

---

## 1. Costs you must say out loud · ~18 min
*Builds on:* nothing — start here

```
You are an expert Python interviewer coaching an advanced developer who already solves algorithm problems and uses lists, dicts, and sets every day.

Teach me how to state real CPython operation costs in a coding interview:
1. For list, dict, set, and collections.deque, give the cost of index, append, pop at each end, and membership. Mark hash costs as average-case, and name the one cost that surprises strong candidates.
2. Show three snippets that look linear and are quadratic: pop or insert at the front of a list, membership tests against a list inside a loop, and string concatenation inside a loop.
3. List the three costs candidates invent: dict lookup is O(log n), set membership is linear, and deque indexing is O(1).
4. Give me a function that builds a result by inserting at index 0 inside a loop. Ask me for the real complexity and the structure I should switch to. Correct me if I'm wrong.
5. End by asking one question: on every element of a list of length n I test `in` against another list of length n. Ask me for the complexity and what I replace the second list with. Wait for my answer before confirming.
```

---

## 2. Hash-map problem patterns · ~22 min
*Builds on:* #1 (what a dict actually costs)

```
You are an expert coding-interview coach for Python, teaching an advanced developer who can already price list, dict, and set operations and who has solved array problems before.

Teach me the hash-map patterns interviewers expect, as choices rather than recipes:
1. Explain when to store a count, when to store an index, and when to store the complement still needed. One decision rule for each.
2. Show three short problems and the map each one wants: two-sum, group anagrams, and longest subarray with a given sum. For each, say what key collision would corrupt the answer.
3. List the three mistakes: using a set when the index is required, overwriting an index you still need, and treating a count map as ordered.
4. Give me this problem: find a contiguous subarray whose elements sum to k, with negative numbers allowed. Ask me what the map stores and what I do on a repeated prefix sum. Correct me if I'm wrong.
5. End by asking one question: the same subarray problem, but every element is positive. Ask me whether the map is still the right tool, and what replaces it. Wait for my answer before confirming.
```

---

## 3. Range invariants · ~22 min
*Builds on:* #2 (you can already decide when a map is enough)

```
You are an expert coding-interview coach, teaching an advanced developer who already chooses hash maps correctly and can price deque operations.

Teach me range invariants used by two pointers and sliding windows:
1. Explain the invariant a two-pointer solution holds on a sorted array, and the invariant a sliding window holds (what is true of the current [left, right] before I move either end).
2. Show three problems: a sorted pair that sums to a target, a window that covers every required character, and a window whose sum stays under a budget. For each, say which end moves and what breaks if I move the other end first.
3. List the three mistakes: shrinking the window before it is valid, forgetting duplicates on a sorted two-pointer scan, and using a list where the window needs pops from the left.
4. Give me longest substring without repeating characters. Ask me to state the invariant and the step that restores it when a repeat appears. Correct me if I'm wrong.
5. End by asking one question: every number is positive and I want the shortest subarray with sum at least k. Ask me which pointer moves when the sum is already large enough, and why a hash map is the wrong tool. Wait for my answer before confirming.
```

---

## 4. Linked-list pointer invariants · ~20 min
*Builds on:* #3 (holding an invariant while a structure changes)

```
You are an expert coding-interview coach, teaching an advanced developer who already writes loop invariants and who has used Python list nodes of the form `class Node: next, value`.

Teach me pointer rewiring, not linked-list vocabulary:
1. Explain why a dummy head removes a special case, and what must stay true of `prev` and `curr` in a reversal before each hop.
2. Show three operations and the one pointer assignment that candidates order wrong: reverse a whole list, remove the n-th node from the end, and detect a cycle with two speeds.
3. List the three mistakes: losing the rest of the list by overwriting `next` too early, advancing a pointer you still need to splice, and using an index as if the list were an array.
4. Give me a singly linked list and ask me to reverse it in place. Ask me to write the three assignments inside the loop in order, then the return value. Correct me if I'm wrong.
5. End by asking one question: after a reversal, which node is the head, and what is `next` on the old head? Wait for my answer before confirming.
```

---

## 5. Monotonic stack · ~20 min
*Builds on:* #4 (rewiring state without losing the rest)

```
You are an expert coding-interview coach, teaching an advanced developer who can hold a pointer invariant and who uses stacks in Python lists.

Teach me monotonic stacks as one invariant:
1. Explain what a decreasing stack of indexes guarantees about every index still on the stack, and why the values I pop are exactly the ones whose answer I now know.
2. Walk next-greater-element, daily temperatures, and largest rectangle in a histogram. For each, say whether the stack is increasing or decreasing and what the popped index's answer is.
3. List the three mistakes: storing values instead of indexes, popping the current element before recording the answer, and forgetting a final drain of the stack at the end of the array.
4. Give me daily temperatures. Ask me what the stack stores and what I record when I pop. Correct me if I'm wrong.
5. End by asking one question: the array is strictly decreasing. Ask me what the stack contains at the end and what every answer is. Wait for my answer before confirming.
```

---

## 6. Binary search and bisect · ~22 min
*Builds on:* #3 (range invariants on a line)

```
You are an expert coding-interview coach, teaching an advanced developer who already maintains range invariants and who has called `bisect` at least once.

Teach me binary search as a predicate, including search on the answer:
1. Explain an inclusive `lo, hi` loop: what is true of `lo` and `hi` at the start of each iteration, and how that differs from `bisect_left` versus `bisect_right` when duplicates exist.
2. Show three cases: exact search in a sorted array with duplicates, first true in a monotonic predicate, and minimum feasible capacity (search on the answer). State the predicate for each.
3. List the three mistakes: an infinite loop from rounding `mid`, moving the wrong bound so the predicate is no longer monotonic, and using binary search on an unsorted predicate.
4. Give me: split an array into k contiguous parts so the largest part-sum is minimized. Ask me for the search bounds and the predicate. Correct me if I'm wrong.
5. End by asking one question: the value occurs three times. Ask me what `bisect_left` and `bisect_right` each return, and how I get the count from them. Wait for my answer before confirming.
```

---

## 7. Interval merge and sweep · ~18 min
*Builds on:* #6 (bounds and sorted order)

```
You are an expert coding-interview coach, teaching an advanced developer who is comfortable with sorted bounds and binary search.

Teach me interval problems as a sort plus one sweep rule:
1. Explain why sorting by start time is the usual first move, and the exact overlap test between the current interval and the last kept interval, including intervals that merely touch.
2. Show three problems: merge overlapping intervals, insert an interval into an already merged list, and find the minimum number of meeting rooms. For meeting rooms, say why a sort of endpoints beats a nested scan.
3. List the three mistakes: sorting by end time and then merging as if you had sorted by start, treating a touch (`end == next start`) as overlap when the problem says half-open, and updating the wrong endpoint when a merge extends the range.
4. Give me a list of [start, end] meetings. Ask me how I compute the minimum rooms, including the events I sort. Correct me if I'm wrong.
5. End by asking one question: two intervals [1, 4] and [4, 5], and the problem says a meeting that ends at t frees the room at t. Ask me whether they conflict, and why. Wait for my answer before confirming.
```

---

## 8. What a tree recursion returns · ~22 min
*Builds on:* #4 (invariants across structure)

```
You are an expert coding-interview coach, teaching an advanced developer who writes recursive functions and knows a binary tree node has left, right, and value.

Teach me how to choose the return value of a tree recursion:
1. Explain the difference between returning a value to the parent, writing into an accumulator, and returning a pair when the parent needs two different answers (best through this node, best anywhere in this subtree).
2. Show three problems and the return each needs: max depth, validate BST (and what bounds travel down), and binary tree maximum path sum (the pair, and why a negative child is dropped).
3. List the three mistakes: passing a path list that aliases across siblings, using a global and forgetting to undo it, and treating a missing child as value 0 in a BST check.
4. Give me the maximum path sum problem. Ask me what the function returns to its parent versus what it records as the global answer. Correct me if I'm wrong.
5. End by asking one question: a node has two negative children. Ask me what it returns upward, and whether those children can still be the global answer on their own. Wait for my answer before confirming.
```

---

## 9. Graph search state · ~22 min
*Builds on:* #8 (recursive structure, then arbitrary edges)

```
You are an expert coding-interview coach, teaching an advanced developer who can choose tree-recursion return values and who represents graphs as adjacency dicts.

Teach me the state that makes a graph search correct:
1. Explain when to mark a node visited on enqueue versus on dequeue, how a directed cycle check needs three colors rather than a boolean, and what Kahn's algorithm uses as its queue.
2. Show three problems: shortest path in an unweighted graph, course schedule (detect a cycle and produce an order), and number of islands on a grid. For each, say what "visited" prevents.
3. List the three mistakes: marking visited only after processing so BFS explodes, using a boolean visited on a directed graph and missing a back edge, and forgetting that grid neighbors can fall off the board.
4. Give me n courses and a list of prerequisite pairs. Ask me how I detect that no ordering exists. Correct me if I'm wrong.
5. End by asking one question: an undirected edge list contains the edge twice, once each way. Ask me what I store in the adjacency map so BFS still terminates. Wait for my answer before confirming.
```

---

## 10. Heaps versus a full sort · ~20 min
*Builds on:* #1 (operation costs) and #9 (priority during a search)

```
You are an expert Python interviewer, teaching an advanced developer who prices builtins correctly and has used `heapq` at least once. Skip the definition of a heap.

Teach me when a heap is the interview answer and how Python's heapq behaves:
1. Explain when k smallest wants a heap, when a full Timsort is the better answer, and how tuple keys give you a min-heap with a tie-break. State that heapq is a min-heap.
2. Show three uses: k most frequent, merge k sorted lists, and Dijkstra on a weighted graph. For each, say what the tuple is and the cost in terms of n and k.
3. List the three mistakes: indexing the heap as if it were sorted, negating a key that is not a number, and pushing items and only heaping once at the end when the point was online processing.
4. Give me "streaming median of integers as they arrive." Ask me how many heaps I keep and what invariant each holds. Correct me if I'm wrong.
5. End by asking one question: k equals n and I need the items in order. Ask me which tool I use and the complexity I state. Wait for my answer before confirming.
```

---

## 11. Backtracking and undo · ~22 min
*Builds on:* #8 and #9 (searching a space you can leave)

```
You are an expert coding-interview coach, teaching an advanced developer who already writes recursive search and understands visited state.

Teach me backtracking as choose, explore, undo:
1. Explain what must be undone on the way back, how sorting plus a skip handles duplicate answers, and what a prune is allowed to assume.
2. Show three problems: subsets, permutations of a list that contains duplicates, and combination sum where each number may be reused. For each, say where the append happens and where the pop happens.
3. List the three mistakes: appending a list that later mutates (aliasing the partial path), skipping duplicates by set insertion after generation instead of pruning, and reusing an element in permutations.
4. Give me subsets of a list that contains duplicates, unique subsets only. Ask me for the sort and the skip condition. Correct me if I'm wrong.
5. End by asking one question: I pass the same `path` list into every recursive call and append it to the answer. Ask me what every stored subset looks like at the end, and the one copy that fixes it. Wait for my answer before confirming.
```

---

## 12. DP state design · ~22 min
*Builds on:* #11 (the search tree you are now collapsing)

```
You are an expert coding-interview coach, teaching an advanced developer who can write a correct backtracking search and explain its tree.

Teach me dynamic programming as a state decision, not as a table you memorize:
1. Explain how you pick the state (index, remaining capacity, or interval), what overlapping subproblems look like in the backtracking tree, and how you know the fill order.
2. Walk three problems and name only the state and the transition: house robber, 0/1 knapsack, and longest increasing subsequence. Say which one is not helped by a 2D table of the naive form.
3. List the three mistakes: a state that forgets a dimension the transition needs, a recurrence that double-counts an item, and computing a cell before one of its dependencies.
4. Give me: coin change, minimum coins for amount, unlimited supply of each coin. Ask me for the state, the transition, and the value that means "impossible." Correct me if I'm wrong.
5. End by asking one question: the same coins, but each coin may be used at most once. Ask me what changes in the loop order, and why the old order overcounts. Wait for my answer before confirming.
```

**Language round**

---

## 13. The hash and equality contract · ~18 min
*Builds on:* #2 (dicts you already depend on)

```
You are an expert in Python's data model, teaching an advanced developer who uses dicts, sets, and custom classes in production. Skip the introduction to those types.

Teach me the hash/equality contract the way a senior interview probes it:
1. Explain why equal objects must share a hash, why that hash must stay stable while the object sits in a dict or set, and when `is` is the comparison you actually want.
2. Show three snippets: a frozen value object used as a key, a class that defines `__eq__` and becomes unhashable, and an object mutated after insertion so lookup misses.
3. List the three mistakes: mutating a key field, defining `__eq__` with no `__hash__` policy, and using `is` on strings or integers.
4. Give me one small class that is unsafe as a set member. Ask me which method is wrong and how I would repair it. Correct me if I'm wrong.
5. End by asking one question: I insert an object into a set, then change a field that both `__eq__` and `__hash__` use. Ask me whether `obj in s` is reliable afterward, and why. Wait for my answer before confirming.
```

---

## 14. Aliasing and shallow copies · ~18 min
*Builds on:* #13 (objects that several containers can see)

```
You are an expert in Python's object model, teaching an advanced developer who already respects the hash contract and who nests lists and dicts inside other containers.

Teach me aliasing as the bug behind a large share of "my algorithm was right" failures:
1. Explain what assignment binds, what a slice or a `dict()` copy actually duplicates, and when only a deep copy separates inner objects.
2. Show three snippets: two names for one list, a copied dict whose nested list is still shared, and a function that mutates its argument so the caller sees the change.
3. List the three mistakes: believing `b = a` copies, believing a slice is deep, and copying a board or path in backtracking with `path.copy()` when the cells themselves are lists.
4. Give me a 2D board built as `[[0] * n] * n`. Ask me what a write to `board[0][0]` does to the other rows, and how I build an independent board. Correct me if I'm wrong.
5. End by asking one question: I copy a dict of lists with `dict(original)` and append to one of the lists through the copy. Ask me whether the original sees that append, and why. Wait for my answer before confirming.
```

---

## 15. When names and defaults are bound · ~18 min
*Builds on:* #14 (shared mutable state)

```
You are an expert Python interviewer, teaching an advanced developer who already uses closures and writes loops that build callbacks. Do not explain what a closure is from scratch.

Teach me binding time as one idea with two traps:
1. Explain when a closure reads a variable (at call time) and when a default argument is evaluated (at definition time).
2. Show three snippets: a loop of lambdas that all see the final index, the same loop fixed with a default argument, and a function whose mutable list default accumulates across calls.
3. List the three weak answers: writing `lambda i=i` without saying why it works, reaching for `nonlocal` when the name is only read, and claiming the mutable default creates a new list on every call.
4. Show me one loop of lambdas and one function with a list default. Ask me to predict both outputs before I rewrite either. Correct me if I'm wrong.
5. End by asking one question: fix a callback-in-a-loop bug using only a default argument, and say which value each callback captured. Wait for my answer before confirming.
```

---

## 16. MRO and super · ~20 min
*Builds on:* #13 (invariants on objects in a hierarchy)

```
You are an expert in Python's object model, teaching an advanced developer who writes class hierarchies and has called `super()` without drawing the MRO. Skip the syntax of writing a class.

Teach me cooperative multiple inheritance:
1. Explain what C3 linearization guarantees, why `super()` follows the MRO of the instance's class rather than the textual parent, and what breaks if one class in the diamond does not call `super()`.
2. Show three hierarchies: a single inheritance chain where `super()` still matters because a mixin may be inserted later, a diamond where both parents call `super()`, and the same diamond where one parent calls its base by name and a method runs twice or not at all.
3. List the three mistakes: assuming `super()` means "my superclass," omitting `super()` in the middle of a cooperative chain, and depending on the order of base classes without being able to state the MRO.
4. Give me classes A, B(A), C(A), D(B, C), each with a method that prints its name and calls `super()`. Ask me for the print order of `D().method()`. Correct me if I'm wrong.
5. End by asking one question: I swap D's bases to `D(C, B)`. Ask me what changes in the MRO and which class now runs before the other. Wait for my answer before confirming.
```

---

## 17. Decorators you write on a whiteboard · ~20 min
*Builds on:* #15 (closures and default binding)

```
You are an expert in Python function objects, teaching an advanced developer who can explain late-binding closures and default-argument capture and who has used simple decorators. Skip the definition of a decorator.

Teach me how to write and critique one under interview conditions:
1. Explain the application order of three stacked decorators, and why a decorator that takes arguments is a function that returns a decorator.
2. Show three versions: a timing decorator that uses functools.wraps, the same decorator without wraps and what breaks for name and signature, and a decorator factory with one parameter.
3. List the three review comments: dropping wraps, forgetting to return the wrapped function's result, and wrapping a method while ignoring `self`.
4. Ask me to write `retry(times)`, which re-invokes the wrapped function on exception up to N times and then re-raises. Review my version for wraps, the return value, and the final exception. Correct me if I'm wrong.
5. End by asking one question: given `@a` above `@b` above `@c` above `def f`, ask me the order of entry and the order of return. Wait for my answer before confirming.
```

---

## 18. Exceptions, EAFP, and chaining · ~18 min
*Builds on:* #17 (wrappers that can swallow failures)

```
You are an expert in Python's exception model, teaching an advanced developer who already writes try/except in production and who can write a decorator. Skip the syntax tour.

Teach me how a senior answers exception questions:
1. Explain EAFP versus checking beforehand, what `raise ... from` preserves, and why catching `Exception` is a different decision from catching `BaseException`.
2. Show three snippets: a file open that asks for forgiveness, a bare `except:` that swallows `KeyboardInterrupt`, and a re-raise that drops the original cause because `from` was omitted.
3. List the three mistakes: using exceptions for ordinary control flow in a tight loop without saying the cost, catching `Exception` around a large block and logging nothing, and cleaning up with a bare except that then continues.
4. Give me a function that parses one record and a caller that parses a batch. Ask me which errors the parser should raise and which the batch loop should catch so one bad record does not kill the batch. Correct me if I'm wrong.
5. End by asking one question: a decorator retries on `Exception`. Ask me whether a `CancelledError` or `KeyboardInterrupt` is included, and what I should catch instead. Wait for my answer before confirming.
```

---

## 19. Context managers and suppressed errors · ~18 min
*Builds on:* #18 (how exceptions propagate)

```
You are an expert in Python's with-statement protocol, teaching an advanced developer who already reasons about exception propagation and writes resource-handling code. Skip the introduction to `with`.

Teach me context managers as a resource protocol with one dangerous return value:
1. Explain when `__enter__` and `__exit__` run, what the three arguments to `__exit__` mean, and what returning true from `__exit__` does to the exception.
2. Show three implementations: a class that closes a resource in `__exit__`, a `@contextmanager` generator that must use `try/finally`, and an `__exit__` that returns True and hides a bug.
3. List the three mistakes: yielding inside the generator before the `try`, returning True by default, and acquiring two resources in one manager so the second failure skips releasing the first.
4. Give me a manager that times a block and must always print the elapsed time, even when the block raises. Ask me where the print goes and what `__exit__` returns. Correct me if I'm wrong.
5. End by asking one question: the block raises, and `__exit__` returns True. Ask me whether the caller sees the exception, and what I change so the caller does see it. Wait for my answer before confirming.
```

---

## 20. Generators, exhaustion, and cleanup · ~20 min
*Builds on:* #19 (cleanup that must run on the failure path)

```
You are an expert in Python's iteration protocol, teaching an advanced developer who writes production loops and decorators and who has used `yield` without reasoning about lifetime.

Teach me generators as an interview topic:
1. Explain the difference between an iterator object and a generator function, and the difference between a generator that is exhausted and one that has been closed.
2. Show three snippets: a generator streaming a large sequence, a generator whose `try/finally` releases a resource, and a generator that receives a value with `send`, plus one sentence on how that differs from a coroutine you `await`.
3. List the three mistakes: iterating a generator twice, building a million-row list when the consumer can pull, and relying on garbage collection to run `finally`.
4. Give me a function that returns a fully built list of a million rows. Ask me to rewrite consumption so memory stays flat, and to say how I release a resource if I stop halfway. Correct me if I'm wrong.
5. End by asking one question: a `for` loop breaks halfway through a generator that opened a resource inside `try/finally`. Ask me whether `finally` has run, and which call guarantees it. Wait for my answer before confirming.
```

---

## 21. Protocols and type signatures · ~20 min
*Builds on:* #16 (nominal hierarchies versus structural fit)

```
You are an expert in Python typing, teaching an advanced developer who annotates function signatures and has used abstract base classes. Skip the history of typing.

Teach me structural typing the way a senior design review uses it:
1. Explain when a `Protocol` is a better contract than an ABC, what a type checker checks that `isinstance` does not, and the lie `@runtime_checkable` can tell you.
2. Show three signatures: a function that accepts any object with `read(self) -> str`, a generic cache of `K` to `V` with `K` bound as hashable, and an `Optional` that callers forget to narrow before use.
3. List the three mistakes: inheriting from a Protocol just to satisfy the checker, using `Any` to silence a real mismatch, and annotating a mutable default with a type while still creating one shared list.
4. Give me a "storage" dependency with `get` and `put`. Ask me to write the Protocol and one sentence on why the concrete class need not inherit from it. Correct me if I'm wrong.
5. End by asking one question: the Protocol is `@runtime_checkable` and a class happens to have a method of the same name with a different meaning. Ask me what `isinstance` returns and what the type checker is actually for. Wait for my answer before confirming.
```

---

## 22. What the GIL serializes · ~18 min
*Builds on:* #20 (lazy pure-Python pipelines you might try to speed up)

```
You are an expert in CPython internals, teaching an advanced developer who ships threaded and async services and knows the syntax of threading, multiprocessing, and async/await. Do not introduce those APIs.

Teach me the Global Interpreter Lock as a senior interview answer:
1. Explain what the GIL serializes on the default build, and what it does not give you: application-level thread safety, or a speedup for pure-Python CPU work.
2. Give three scenarios and what happens to wall-clock time as thread count rises: blocking I/O, a tight pure-Python CPU loop, and a C extension that releases the GIL during the heavy call.
3. Name the three claims candidates get wrong: the GIL makes code thread-safe, threads never help, and the free-threaded build available since 3.13 is what you get by default.
4. Give me one workload in two sentences. Ask me whether threads, on the default build, will cut wall-clock time. Correct me if I'm wrong.
5. End by asking one question: predict throughput of a pure-Python CPU loop going from 1 thread to 8 on the default build, and say what would have to change about the build or the code for that prediction to flip. Wait for my answer before confirming.
```

---

## 23. Choosing threads, processes, or asyncio · ~20 min
*Builds on:* #22 (what the GIL does on the default build)

```
You are an expert in Python concurrency, teaching an advanced developer who knows the default GIL serializes bytecode, that blocking I/O can release it, and that processes have separate interpreters. Do not reteach syntax or the GIL.

Teach me how to pick one tool and reject the other two:
1. For each pressure — pure-Python CPU work, blocking I/O, a very large number of sockets, shared mutable memory, startup and pickle cost — say which tool wins and the cost that disqualifies the others.
2. Walk three workloads: resizing 2,000 images, fetching 1,000 URLs, and a service that does a heavy pure-Python scoring step per request while holding many open connections. Name the runner-up's failure mode each time.
3. List the three justifications interviewers punish: "asyncio is faster" with no workload, sharing a live socket or lock across processes, and ignoring the pickle boundary.
4. Give me a new two-sentence workload. Ask me to pick one tool and to say what I refuse to share across workers. Correct me if I'm wrong.
5. End by asking one question: the workload changes from many slow HTTP calls to one tight numerical loop over a large in-memory list. Ask what I switch to, and what I must explicitly hand each worker. Wait for my answer before confirming.
```

---

## 24. Asyncio failure modes · ~22 min
*Builds on:* #23 (the tool choice) and #20 (generators versus coroutines)

```
You are an expert in asyncio, teaching an advanced developer who writes `async def` code and already knows the default GIL story. Skip the event-loop introduction.

Teach me the failure modes that decide senior asyncio interviews:
1. Explain why one blocking call inside a coroutine stalls every other task on that loop, and how cancellation is delivered: a `CancelledError` at an await point, with cleanup in `finally` or a task group.
2. Show three snippets: a blocking HTTP or sleep call inside `async def`, `asyncio.gather` when one task fails with `return_exceptions` false versus true, and a coroutine that catches `CancelledError` and swallows it.
3. List the three mistakes: expecting `async` to speed a pure-Python CPU loop, creating tasks you never await so failures surface later as an unretrieved exception, and holding a lock across a cancellation point with no cleanup.
4. Give me a coroutine of about 15 lines that fetches URLs and also runs a heavy pure-Python checksum. Ask me to point at the line that blocks the loop and say what I would move off the loop. Correct me if I'm wrong.
5. End by asking one question: a task is cancelled while it is inside a blocking socket read that was called with no `await`. Ask me whether cancellation takes effect immediately, and why. Wait for my answer before confirming.
```

**Design round**

---

## 25. Design an in-process LRU · ~22 min
*Builds on:* #1 (costs), #13 (keys), #17 (a small public API)

```
You are a senior Python interviewer in an API-design round. I can price dict operations, honor the hash contract, and write a small class. Do not reteach those.

Run a design session for one type: an in-process LRU cache with a fixed capacity.
1. Ask me for the public methods, the complexity I promise for get and put, and the structure pair I use. Push back if I reach for a sort on every get.
2. After I answer, show a design you would accept: ordered mapping for recency, what happens at capacity, and what get does to recency. Call out thread safety as a separate promise I must either make or refuse.
3. Give me three edge cases: capacity 1, put of a key that exists, and a value that is itself mutable. Ask me which of those my design gets wrong.
4. End by asking one question: two threads call get and put with no external lock. Ask me what I can honestly guarantee on the default CPython build, and the one sentence I would add to the docstring. Wait for my answer before confirming.
```

---

## 26. What to test and what to fake · ~20 min
*Builds on:* #25 (a design you can now pin down with tests)

```
You are a senior Python engineer reviewing tests, teaching an advanced developer who writes pytest and has used mocks. Skip the pytest syntax tour.

Teach me how an interview tests a small component:
1. Explain which collaborators you fake (clock, network, random) and which behavior you assert through the public API of the object under test.
2. Show three tests for the LRU from a typical interview: capacity eviction order, updating an existing key, and a caller who mutates a value after put. Say what a mock would hide in each.
3. List the three weak tests: asserting the call order of private methods, a test that reimplements the function, and a flaky test that sleeps.
4. Give me a rate limiter whose decision depends on time. Ask me what I inject and which three cases I assert (allowed, denied, allowed again after the window). Correct me if I'm wrong.
5. End by asking one question: the implementation switches from a dict to an ordered dict, and behavior is unchanged. Ask me which tests should still pass without edits, and which assertions were too tightly bound to the old structure. Wait for my answer before confirming.
```

---

## 27. SQL access paths · ~22 min
*Builds on:* #1 (you already talk about cost)

```
You are an expert in relational databases, teaching an advanced Python developer who writes queries through an ORM or a driver and already knows SELECT, JOIN, and WHERE. Skip introductory SQL.

Teach me how to talk about an access path in a backend interview:
1. Explain a leftmost index prefix, why a condition on the second column of a composite index may not seek, and what a covering index avoids.
2. Show three query shapes and the index you would add: equality on user_id plus ORDER BY created_at, a filter on a low-selectivity boolean, and an ORM loop that issues one query per parent row.
3. List the three mistakes: indexing every column independently and expecting the planner to combine them as one seek, selecting every column when the index could cover the query, and calling the N+1 pattern "fine because each query is indexed."
4. Give me a table of events (user_id, created_at, type) and the query "latest 20 events for a user of a given type." Ask me for the index and the one column I would leave out of it. Correct me if I'm wrong.
5. End by asking one question: the predicate is `WHERE lower(email) = lower(%s)`. Ask me why a plain index on email does not serve it, and what kind of index does. Wait for my answer before confirming.
```

---

## 28. Transactions and lost updates · ~20 min
*Builds on:* #27 (you can already get the rows)

```
You are an expert in relational transactions, teaching an advanced Python developer who can choose an index and who writes multi-statement updates from application code.

Teach me the anomalies a backend interview expects you to name:
1. Explain lost update, what READ COMMITTED still allows, and how a unique constraint plus a single INSERT gives you an idempotency guarantee a check-then-insert does not.
2. Show three flows: two workers incrementing a balance by read-modify-write, a check-then-insert of a webhook delivery row, and a transfer that debits one row and credits another. Say where the transaction boundary goes.
3. List the three mistakes: holding a transaction open across an HTTP call, bumping the isolation level when a constraint would do, and catching a unique violation and then continuing as if the write succeeded without reading the winner.
4. Give me two workers creating a delivery row for the same (endpoint, event_id). Ask me for the constraint and the application behavior on conflict. Correct me if I'm wrong.
5. End by asking one question: the balance update is `SET balance = balance + %s` inside one statement. Ask me whether a lost update is still possible, and why the read-modify-write version is different. Wait for my answer before confirming.
```

---

## 29. Cache invalidation for one endpoint · ~20 min
*Builds on:* #25 (LRU mechanics) and #28 (the database remains the source of truth)

```
You are a senior backend interviewer, teaching an advanced Python developer who can design an in-process cache and state a transaction boundary.

Teach me caching for one read-heavy endpoint:
1. Explain the choice between a TTL and explicit invalidation, what a cache stampede is, and why the cache key must include every input that changes the response.
2. Show three designs for "GET /users/{id}/profile": a 30-second TTL, invalidate on write to that user, and a request-collapsing lock so 500 concurrent misses do not all hit the database. State the stale-read behavior of each.
3. List the three mistakes: caching a response that includes the caller's permissions under a key that omits the caller, deleting the wrong key on write, and treating an in-process cache as coherent across several app processes.
4. Give me a profile that changes when either the user row or the user's team row changes. Ask me for the keys I invalidate on each write. Correct me if I'm wrong.
5. End by asking one question: I run four app processes, each with its own dict cache, and I invalidate only inside the process that handled the write. Ask me what the other three serve, and the one shared store that fixes it. Wait for my answer before confirming.
```

---

## 30. Jobs, retries, and idempotency · ~20 min
*Builds on:* #24 (work that must leave the request) and #28 (constraints)

```
You are a senior backend interviewer, teaching an advanced Python developer who can place a transaction boundary and describe asyncio's limits. Skip the tutorial for any specific queue product.

Teach me at-least-once work:
1. Explain why a retry implies the handler may run twice, what an idempotency key stores, and how a visibility timeout interacts with a handler that runs longer than the timeout.
2. Show three failures: a handler that sends a webhook and then crashes before ack, a handler that acks before the side effect, and a poison message that fails forever. Say what the queue and the handler should do in each.
3. List the three mistakes: a retry with no backoff, a side effect with no idempotency key, and an attempt counter stored only in process memory.
4. Give me "deliver a webhook, retry up to 8 times, never call the customer twice for the same event." Ask me what I store before the HTTP call and what I do when the call succeeds but the ack fails. Correct me if I'm wrong.
5. End by asking one question: the handler's work sometimes takes longer than the visibility timeout. Ask me what the second worker does when it receives the same message, and which of my idempotency checks stops a double send. Wait for my answer before confirming.
```

---

## 31. Design one service end to end · ~24 min
*Builds on:* #29 and #30 (cache and durable work)

```
You are a senior backend interviewer running a system-design round with an advanced Python developer who can already talk about caches, transactions, and at-least-once jobs. Do not reteach those pieces in the abstract.

Run the design of one system: a multi-tenant webhook delivery service. Producers POST an event; the system delivers it to each tenant's registered HTTPS endpoints and exposes a delivery status.

Conduct it this way:
1. State a traffic number, a latency expectation for the POST, and one failure rule: a slow customer endpoint must not slow the POST or anyone else's deliveries.
2. Ask me to draw the request path, the data I persist, the worker model, and where retries live. Challenge one weak spot: the POST doing the HTTP delivery inline, a missing idempotency key, or status rows with no tenant boundary.
3. After I respond, give the design you would accept, including the Python runtime choice for the worker and the one index the status query needs.
4. End by asking one question: one tenant's endpoint starts timing out on every call and they have 100,000 pending events. Ask me what I isolate so other tenants stay healthy. Wait for my answer before confirming.
```

**Mocks**

---

## 32. Coding mock · ~25 min
*Builds on:* #1 through #12

```
You are a Python coding interviewer. I already price builtins and can apply hash maps, range invariants, pointers, stacks, binary search, intervals, trees, graphs, heaps, backtracking, and DP. Do not teach a pattern up front.

Run one timed problem, interview style:
1. Give me one medium-hard problem that has a plausible wrong first design (a quadratic scan that a map, window, heap, or DP improves). Include duplicates and an empty input in the statement.
2. Ask me to restate the problem, name complexity targets, then write Python. Interrupt once with a failing example if my first idea is wrong. Do not show a solution yet.
3. After I write it, review correctness on the empty input, on duplicates, and on the complexity I claimed, including any hidden quadratic builtin.
4. End by asking one question: change one constraint so my approach no longer meets the target. Ask me what I switch to and the new complexity. Wait for my answer before confirming.
```

---

## 33. Language autopsy · ~24 min
*Builds on:* #13 through #24

```
You are a senior Python interviewer running a code-review round. I already understand hashing, aliasing, binding time, MRO, decorators, exceptions, context managers, generators, protocols, the GIL, concurrency choice, and asyncio cancellation. Do not reteach those.

Give me one self-contained snippet of about 45 lines: a small service class whose bugs interact. Include a late-bound callback, a mutable key in a set, a shallow copy of nested config, a decorator that swallows a cancellation or a return value, and a blocking call on an event loop. Do not label the bugs.

Run it this way:
1. Ask me to find each bug and describe the user-visible failure. Do not hint.
2. After I answer, confirm or correct each one and show the smallest fix.
3. Ask me which bug I would fix first in production, and respond to my reasoning.
4. End by asking one question: after the fixes, the hot path becomes pure-Python CPU work across many files. Ask what I change about the runtime and what I stop sharing across workers. Wait for my answer before confirming.
```

---

## 34. Design defense · ~22 min
*Builds on:* #31 (a full service you can now defend)

```
You are a senior interviewer in the second half of a design round. I can already sketch a webhook delivery system with a fast POST, durable retries, and per-tenant isolation. Do not reteach that design from zero.

Pressure-test my design:
1. Restate the system in four lines, then give me three changes, one at a time: POST latency budget drops to 50 ms at 2,000 requests per second, payloads can be 5 MB, and customers demand exactly-once effects on their side even though the network cannot provide it.
2. After each change, ask me what moves, what I refuse to promise, and which data store or Python runtime choice flips.
3. Then give the answers you would accept, including the exact promise I should make instead of "exactly once."
4. End by asking one question: the queue backs up for a single tenant while everyone else is healthy. Ask me the signal I page on, and the control I give an operator that does not drop another tenant's events. Wait for my answer before confirming.
```

---

## 35. Tell a production incident · ~18 min
*Builds on:* #34 (you can already defend a design; now defend a real decision)

```
You are a hiring manager running the experience round with an advanced Python developer. I can discuss runtime and design trade-offs. Do not teach a postmortem framework up front.

Interview me about one production incident:
1. Ask me to pick a real incident I handled in a Python service. If I do not have one, use this case and make me investigate it out loud: after a deploy, p99 jumped, and the diff added synchronous HTTP inside a per-item loop plus JSON logging of full payloads.
2. Push on evidence: what I measured, what I ruled out, and why the first hypothesis was wrong. Reject answers that name a tool and skip the observation.
3. After I finish, tell me the two missing pieces a strong interviewer still wanted, then show a tight version of the story: symptom, evidence, mechanism, change, and what I checked afterward.
4. End by asking one question: the same bug is proposed again six months later under a deadline. Ask me the one-sentence technical objection I would raise, tied to a measurement. Wait for my answer before confirming.
```
