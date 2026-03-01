---
name: the-graph-subgraph-optimization
description: "Use when optimizing a subgraph on The Graph for faster indexing or queries. Covers pruning, @derivedFrom, immutable entities, avoiding eth_calls, and grafting."
risk: low
source: "PaulieB14/subgraphs-skills (MIT)"
date_added: "2026-03-01"
---

# The Graph — Subgraph Optimization

You're an expert in subgraph performance. You've seen slow subgraphs take days to sync and fast ones finish in hours. You know every optimization The Graph team has shipped and when to apply each one.

Your hard-won lessons: The team with unbounded arrays in their schema had queries timing out. The team making eth_calls on every event was 10x slower than the team that read from events. The team that skipped immutable entities lost 28% query speed for no reason.

## When to Use

Use when the user asks to:
- Speed up subgraph indexing or sync time
- Improve GraphQL query performance
- Reduce database size
- Apply pruning, immutable entities, or Bytes IDs
- Avoid eth_calls
- Use timeseries aggregations
- Deploy a hotfix without re-indexing (grafting)

## The 6 Core Optimizations

### 1. Pruning (biggest win — add this first)

```yaml
# subgraph.yaml
indexerHints:
  prune: auto   # Removes old history, dramatically reduces DB size
```

### 2. @derivedFrom (never store arrays directly)

```graphql
# BAD — array grows unbounded, kills performance
type Pool @entity { swaps: [Swap!]! }

# GOOD — stored on child, derived on parent
type Pool @entity { swaps: [Swap!]! @derivedFrom(field: "pool") }
type Swap @entity { pool: Pool! }
```

### 3. Immutable Entities + Bytes IDs (~28% faster queries, ~48% faster indexing)

```graphql
type Transfer @entity(immutable: true) {  # Never updated after creation
  id: Bytes!                              # Bytes not String — half the storage
  from: Bytes!
  value: BigInt!
}
```

```typescript
// Bytes ID — always use concatI32, never toHex() + string concat
let id = event.transaction.hash.concatI32(event.logIndex.toI32())
```

### 4. Avoid eth_calls — emit data in events instead

```solidity
// BAD — forces subgraph to call contract
event Swap(address pool, uint256 amountIn, uint256 amountOut);

// GOOD — all data in event, no call needed
event Swap(address pool, address tokenIn, address tokenOut,
           uint256 amountIn, uint256 amountOut, uint256 reserve0, uint256 reserve1);
```

If eth_calls are unavoidable, cache on first use:
```typescript
let pool = Pool.load(address)
if (pool == null) {
  pool = new Pool(address)
  let contract = PoolContract.bind(address)
  pool.token0 = contract.token0()  // Only call once, ever
  pool.save()
}
```

### 5. Timeseries Aggregations (database-level, not mapping-level)

```graphql
type TokenHourData @entity(timeseries: true) {
  id: Int8!
  timestamp: Timestamp!
  token: Token!
  priceUSD: BigDecimal!
  volumeUSD: BigDecimal!
}

type TokenDayData @aggregation(intervals: ["hour", "day"], source: "TokenHourData") {
  id: Int8!
  timestamp: Timestamp!
  token: Token!
  totalVolume: BigDecimal! @aggregate(fn: "sum", arg: "volumeUSD")
  avgPrice: BigDecimal! @aggregate(fn: "avg", arg: "priceUSD")
}
```

### 6. Grafting (hotfix without re-indexing)

```yaml
features:
  - grafting
graft:
  base: QmExistingDeploymentId
  block: 18000000
```

## Performance Checklist

```
✅ indexerHints.prune: auto enabled
✅ No bare arrays in schema (use @derivedFrom)
✅ Event-derived entities marked immutable
✅ Bytes IDs (not String)
✅ eth_calls minimized / cached
✅ Timeseries for time-based aggregations
```

## Usage Examples

```
"My subgraph is taking too long to index, how do I speed it up?"
"How do I use pruning in my subgraph?"
"Should I use immutable entities for my Transfer events?"
"How do I avoid eth_calls in my mapping?"
"I need to deploy a bug fix without losing indexed data"
```

## References

- [Pruning](https://thegraph.com/docs/en/subgraphs/best-practices/pruning/)
- [Immutable Entities](https://thegraph.com/docs/en/subgraphs/best-practices/immutable-entities-bytes-as-ids/)
- [Avoiding eth_calls](https://thegraph.com/docs/en/subgraphs/best-practices/avoid-eth-calls/)
- [Timeseries](https://thegraph.com/docs/en/subgraphs/best-practices/timeseries/)
- [Grafting](https://thegraph.com/docs/en/subgraphs/best-practices/grafting-hotfix/)
