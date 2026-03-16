# AutoSave Bot – Smart DeFi Savings

## Overview
A full-stack hackathon web application that lets users connect MetaMask and make real on-chain deposits into YO Protocol's yoUSD vault on Base network, plus a DeFi savings simulator.

## Architecture

### Tech Stack
- **Frontend**: React + Vite, TypeScript (ES2020 target), TailwindCSS, Framer Motion
- **Backend**: Express.js, TypeScript, Drizzle ORM
- **Database**: PostgreSQL (Neon/Replit)
- **Blockchain**: viem (Web3 library), MetaMask via window.ethereum

### Key Design Decisions
- Dark fintech theme with deep blue (#3B82F6) primary and purple accent colors
- `glass-panel` CSS utility class for frosted-glass card styling
- No sidebar — single-layout with header/footer in `Layout.tsx`
- `tsconfig.json` target set to `ES2020` for BigInt literal support

## Project Structure

```
client/src/
  pages/
    Home.tsx           # Landing page with hero, stats, features
    Dashboard.tsx      # Main app: YO vault + savings simulator
  components/
    Layout.tsx         # App shell with header/footer
    YoVaultDashboard.tsx  # Real Web3 vault UI (deposit/redeem)
  hooks/
    use-yo-vault.ts    # MetaMask connection + ERC-4626 vault interactions
    use-simulations.ts # API hooks for savings simulator
  lib/
    yo-vault.ts        # viem client setup, contract addresses, ABIs
    queryClient.ts     # TanStack Query setup
  types/
    ethereum.ts        # window.ethereum TypeScript declarations
shared/
  schema.ts           # Drizzle schema: simulations table
server/
  routes.ts           # API: GET/POST /api/simulations
  storage.ts          # Storage interface + DB implementation
  index.ts            # Express server entry
```

## YO Protocol Integration

### On-chain details (Base network, chain ID 8453)
- **yoUSD Vault**: `0x0000000f2eb9f69274678c76222b35eec7588a65` (ERC-4626)
- **USDC (Base)**: `0x833589fcd6edb6e08f4c7c32d4f71b54bda02913` (6 decimals)
- **Vault standard**: ERC-4626 tokenized yield-bearing vault
- **Explorer**: basescan.org

### Deposit Flow
1. Connect MetaMask
2. Switch to Base network (auto-prompts if needed)
3. Approve USDC spending allowance
4. Deposit USDC → receive yoUSD shares (ERC-4626 deposit)

### Redeem Flow
1. Burn yoUSD shares → receive USDC + accrued yield (ERC-4626 redeem)

### Libraries
- `viem` — blockchain interactions (installed)
- `wagmi` — NOT installed (TypeScript version conflict); using raw window.ethereum instead

## Running
- `npm run dev` — starts Express (port 5000) + Vite dev server together
- Workflow: "Start application"
