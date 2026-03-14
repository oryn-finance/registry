# Oryn Registry

Public registry of [Oryn Escrow](https://github.com/oryn-finance/evm-escrow) deployments across EVM chains. Provides contract addresses, supported assets, RPC endpoints, and configuration metadata for each network.

## Structure

```
chains/
  mainnet/
    index.json              List of active mainnet chain IDs
    <chain>.json            Per-chain deployment config
  testnet/
    index.json              List of active testnet chain IDs
    <chain>.json            Per-chain deployment config
```

## Chain Config Schema

Each `<chain>.json` file contains:

| Field            | Type     | Description                                   |
| ---------------- | -------- | --------------------------------------------- |
| `id`             | `string` | Unique chain identifier (e.g. `base_sepolia`) |
| `name`           | `string` | Human-readable chain name                     |
| `chain_id`       | `number` | EVM chain ID                                  |
| `rpc_url`        | `string` | Public RPC endpoint                           |
| `explorer_url`   | `string` | Block explorer base URL                       |
| `icon`           | `string` | Chain icon URL                                |
| `escrow_factory` | `string` | Deployed `EscrowFactory` contract address     |
| `filler_address` | `string` | Filler/relayer address for this chain         |
| `source_expiry`  | `number` | Source-side escrow expiry (seconds)           |
| `dest_expiry`    | `number` | Destination-side escrow expiry (seconds)      |
| `assets`         | `array`  | List of supported assets (see below)          |

### Asset Schema

| Field           | Type     | Description                                      |
| --------------- | -------- | ------------------------------------------------ |
| `id`            | `string` | Asset identifier (e.g. `eth`, `usdc`)            |
| `symbol`        | `string` | Token ticker symbol                              |
| `name`          | `string` | Full token name                                  |
| `decimals`      | `number` | Token decimals                                   |
| `token_address` | `string` | ERC20 contract address (`0xEee...eE` for native) |
| `icon`          | `string` | Token icon URL                                   |
| `cmc_id`        | `number` | CoinMarketCap ID for price lookups               |
| `min_amount`    | `string` | Minimum escrow amount (in smallest unit)         |
| `max_amount`    | `string` | Maximum escrow amount (in smallest unit)         |

## Active Deployments

### Testnet

| Chain            | Chain ID | Explorer                                  |
| ---------------- | -------- | ----------------------------------------- |
| Avalanche Fuji   | 43113    | [snowtrace](https://testnet.snowtrace.io) |
| Arbitrum Sepolia | 421614   | [arbiscan](https://sepolia.arbiscan.io)   |
| Base Sepolia     | 84532    | [basescan](https://sepolia.basescan.org)  |

### Mainnet

Coming soon.

## Usage

Fetch the registry over raw GitHub content or clone locally:

```bash
# List active testnet chains
curl -s https://raw.githubusercontent.com/oryn-finance/oryn-registry/main/chains/testnet/index.json

# Get config for a specific chain
curl -s https://raw.githubusercontent.com/oryn-finance/oryn-registry/main/chains/testnet/base_sepolia.json
```

## Contributing

To add a new chain deployment:

1. Create `chains/{mainnet|testnet}/<chain_id>.json` following the schema above
2. Add the chain ID to the corresponding `index.json`
3. Open a pull request

## License

[MIT](LICENSE)
