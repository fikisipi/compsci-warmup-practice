## `compsci-warmup-practice`: TILs and computer science things.

> [!CAUTION]
> This is not really for public or prod use, does not represent my knowledge -- or lack
thereof! :) ... btw, this scary style can be set with [!CAUTION]

### 12 May

* A good set of precommit hooks for Python - [Example yaml](./repo-health/example-precommit.yaml)
* `brew install tmate` let's you share terminal even inside NAT, conn drops, IP changes.
* `asyncio.create_task` now becomes `TaskGroup().create_task`:
    *  Use `async with asyncio.TaskGroup() as tg:` to await them all
*  `core.excludesFile`: Git looks up `git config core.excludesFile` for `.gitignore`,
so you can have a global gitignore too (by passing the `--global` flag)
* In 2025, Python's `ABC` can be replaced with `typing.Protocol` (more flexible!)
    * Protocol is structurally typed: for a protocol P1, every type T that satisfies the requirements
    is assignable to P1
* Command-query separation - CQRS:
    * CQRS splits responsibilities into returning data (query) and doing an action (command)
    * Used in event sourcing
    * Event sourcing is decomposing program into series of actions that mutate a state.

### Circuit breaker pros

If a program `P` depends on an operation `O_1` not failing, you can retry `O_1`.
But if you retry too much, all programs `P_2`, `P_3`, ... that depend on `O_1` may fail in
a cascade way since `P` is DDoS-ing.

### Strategy vs Resolver:
Suppose an algorithm `A` working on data `D` can be decomposed to sub-algorithms `A11`, `A12`, `A13`.

We can encapsulate this into two things:
* Strategies `S_i`: the contract specifying the input and output of subalgos `A11`, `A12`, `A13`
* A context `C`: a higher-order function replacing `A` that uses the strategies `S_i`
to operate on `D`.

### Modern debugging: log vs metric vs trace

1. A log `L` is a historical record that an event occured.
* Modern logs should be structural.
* An user visit isn't `GET 200 OK 8.55.12.5`, it is `{"ip": .., "country": ..,}
2. When you aggregate numerical properties of logs `L1, L2, .. into sums or averages, you build a *metric*.
* Should not be tried on non-aggregable ops: what's the average of an IP address strign? :)
* Core benefit: perf analysis
* Secondary benefit: business (ex. `orders per hour` metric helps developers but BI people too!)
* Observability: understand system's internal state. Best FOSS tool: OTEL
3.
