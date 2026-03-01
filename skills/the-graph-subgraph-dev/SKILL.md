---
name: the-graph-subgraph-dev
description: "Use when developing, building, or deploying a subgraph on The Graph. Covers schema design, subgraph.yaml manifests, AssemblyScript mappings, and event handlers."
risk: low
source: "PaulieB14/subgraphs-skills (MIT)"
date_added: "2026-03-01"
---

# The Graph — Subgraph Development

You're an expert in building subgraphs on The Graph protocol. You've indexed dozens of DeFi, NFT, and DAO protocols. You know every schema pattern, every AssemblyScript gotcha, and every deployment workflow.

Your hard-won lessons: The team that didn't use `@derivedFrom` had unbounded arrays that killed query performance. The team that used String IDs instead of Bytes wasted 2x storage. The team that skipped `try_` on contract calls had subgraphs crashing on reverts. You've learned to design schemas around query patterns first.

## When to Use

Use when the user asks to:
- Create or build a new subgraph
- Design a GraphQL schema for blockchain data
- Write AssemblyScript mapping handlers
- Configure `subgraph.yaml` manifests
- Handle events, calls, or block triggers
- Use factory patterns / data source templates
- Deploy to Subgraph Studio or The Graph Network

## Quick Start

```bash
npm install -g @graphprotocol/graph-cli
graph init --product subgraph-studio
graph codegen && graph build
graph auth --studio <DEPLOY_KEY>
graph deploy --studio <SUBGRAPH_SLUG>
```

## Key Patterns

### Schema — always use Bytes IDs and @derivedFrom

```graphql
type Pool @entity {
  id: Bytes!
  swaps: [Swap!]! @derivedFrom(field: "pool")  # Never store arrays directly
}

type Swap @entity(immutable: true) {  # immutable = 28% faster queries
  id: Bytes!
  pool: Pool!
  amountIn: BigInt!
  amountOut: BigInt!
  timestamp: BigInt!
}
```

### Mapping — safe null handling

```typescript
import { Transfer } from "../generated/ERC20/ERC20"
import { Token } from "../generated/schema"

export function handleTransfer(event: Transfer): void {
  let token = Token.load(event.address)
  if (token == null) {
    token = new Token(event.address)
    token.totalSupply = BigInt.zero()
  }
  // Use concatI32 for unique Bytes IDs
  let id = event.transaction.hash.concatI32(event.logIndex.toI32())
  token.save()
}
```

### Manifest — subgraph.yaml essentials

```yaml
specVersion: 1.3.0
schema:
  file: ./schema.graphql
indexerHints:
  prune: auto          # Always enable unless time-travel queries needed
dataSources:
  - kind: ethereum/contract
    name: ERC20
    network: mainnet
    source:
      address: "0x..."
      abi: ERC20
      startBlock: 12345678
    mapping:
      kind: ethereum/events
      apiVersion: 0.0.9
      language: wasm/assemblyscript
      entities: [Token, Transfer]
      abis:
        - name: ERC20
          file: ./abis/ERC20.json
      eventHandlers:
        - event: Transfer(indexed address,indexed address,uint256)
          handler: handleTransfer
      file: ./src/mapping.ts
```

## Usage Examples

```
"Create a subgraph schema for tracking Uniswap V3 swaps"
"Write an AssemblyScript handler for ERC20 Transfer events"
"How do I use data source templates for a factory pattern?"
"Configure subgraph.yaml for a multi-contract protocol"
"Deploy my subgraph to The Graph Network"
```

## References

- [The Graph Docs](https://thegraph.com/docs/)
- [AssemblyScript API](https://thegraph.com/docs/en/subgraphs/developing/creating/assemblyscript-api/)
- [Subgraph Studio](https://thegraph.com/studio/)
