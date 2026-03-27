# 🪂 Multi-Chain Airdrop Tracker

An autonomous airdrop monitoring system that tracks your wallet across 14+ EVM chains, discovers new tokens, identifies contract interactions, and monitors project blogs for claim announcements.

## Features

- **Multi-chain monitoring** — Ethereum, Base, Arbitrum, Optimism, Polygon, BSC, Avalanche, zkSync, Scroll, Linea, Blast, Mantle, HyperEVM
- **Token discovery** — Finds all ERC20 tokens via Transfer event logs
- **Protocol identification** — Maps contract interactions to known DeFi protocols via DeFi Llama
- **Transaction intelligence** — Identifies contracts via Etherscan verified source code
- **Scam detection** — Flags phishing tokens automatically
- **Blog/RSS monitoring** — Watches project blogs for airdrop announcements
- **Money engine** — Finds yield opportunities, airdrop candidates, and testnet rewards

## Quick Start

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/airdrop-tracker.git
cd airdrop-tracker

# Install dependencies
npm install

# Configure your wallet
cp config.example.json config.json
# Edit config.json with your wallet address and chains

# Run the tracker
node tracker.js | node format.js

# Run the discovery engine
node discover.js | node format-discover.js

# Run the money engine
cd money-engine
node money-engine.js | node format.js
```

## Configuration

Edit `config.json`:

```json
{
  "wallet": "YOUR_WALLET_ADDRESS",
  "chains": {
    "ethereum": { "rpc": "https://ethereum-rpc.publicnode.com", "chainId": 1, "symbol": "ETH" }
  },
  "watchlist": [
    { "name": "Project Name", "chain": "ethereum", "url": "https://project.com", "blog": "https://project.com/rss" }
  ],
  "scamPatterns": ["visit.*to claim", "claim.*reward"]
}
```

## Components

| File | Description |
|------|-------------|
| `tracker.js` | Balance monitoring + scam detection |
| `discover.js` | Chain discovery + token scanning |
| `tx-intel.js` | Transaction intelligence + contract identification |
| `format.js` | Telegram-friendly output formatter |
| `money-engine/money-engine.js` | Yield + airdrop + testnet scanner |

## Cron Setup (OpenClaw)

```bash
openclaw cron add \
  --name "airdrop-tracker" \
  --cron "0 */6 * * *" \
  --message "Run the airdrop tracker: cd /path/to/tracker && node tracker.js | node format.js" \
  --announce --channel telegram
```

## License

MIT
