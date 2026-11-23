# VANDA

> It blooms through stone.

VANDA is a 3,333-piece NFT collection of orchid specimens on BNB Smart Chain
(BEP-721). Five varieties, sequential Accession Nº 001–3,333, first mint FREE
for any SPACE ID Agent ID holder, max 6 per wallet.

- Site: https://vanda-five.vercel.app/
- Chain: BNB Smart Chain (BSC mainnet, chain ID 56)
- Standard: BEP-721, sequential token IDs 1–3,333
- Language: English only
- Status: **PREVIEW — contracts not deployed yet**

## At a glance

| | |
|---|---|
| Supply | 3,333 |
| Presale | First 333 paid mints @ 0.0001 BNB flat (free mint #1 still runs; auto-closes at 333) |
| Price ladder | After presale: #1 FREE · #2 0.0005 · #3 0.001 · #4 0.002 · #5 0.003 · #6 0.005 BNB |
| Max per wallet | 6 (max 0.0115 BNB per wallet) |
| Gate | SPACE ID Agent ID, every mint (no allowlist) |
| Token | $VANDA — 1B total (540M pool / 460M treasury), 120,000 per paid mint, max 600,000/wallet |
| Royalty | 5% to the owner |
| Marketplace | Own escrow, 0% fee (seller 95% / royalty 5%) |
| baseURI | https://vanda-five.vercel.app/metadata/ |

## Rarity

| Tier | Variety | Accession Nº | Count | Share |
|---|---|---|---|---|
| Common | Vanda Alba | 001–1,666 | 1,666 | 50.0% |
| Uncommon | Vanda Rosea | 1,667–2,499 | 833 | 25.0% |
| Rare | Vanda Coerulea | 2,500–2,999 | 500 | 15.0% |
| Epic | Vanda Aurea | 3,000–3,249 | 250 | 7.5% |
| Legendary | Miss Joaquim | 3,250–3,333 | 84 | 2.5% |

IDs are sequential in mint order — the variety of a token follows its
Accession number. The Legendary Miss Joaquim is the 1893 Singapore hybrid
(Vanda hookeriana × Vanda teres), Singapore's national flower.

## Contracts (PREDICTED — not deployed yet)

| Contract | Predicted address |
|---|---|
| VandaToken ($VANDA) | 0xF4390D14A2B599833e19b135cE9aD3Ae5Db4AECe |
| VandaNFT (VANDA) | 0x0C4E3e87eB1194706822Cc7074B4c229F1da0419 |
| VandaMarketplace | 0x5b6D7F4D89262a025ffdBd518e37FEF37316dd28 |

Owner / treasury / royalty receiver:
0x7379CA652f68fd1daAc11b7b87bb6B222fD129fa

Deploy order: token → NFT → marketplace, from the paired wallet
0x05f63E20097c9360D9D68277b90b4a8A8cF8D7C1. Wiring: `setMinter(NFT)` once on
the token, then `transferOwnership(new wallet)`. Mint opens at deploy.
Est. deploy gas 4,094,151 ≈ 0.0002047 BNB @ 0.05 gwei. Full prediction
record: `contracts/vanda_predictions.md`.

## Minting (for agents)

Minting is AGENT-ONLY: no wallet button on the page, no browser
transactions — copy the free-mint or paid/batch prompt from the mint panel
and give it to your agent. See `SKILL.md` for the full agent mint skill:
presale-aware free-mint and batch-mint prompts, selectors, and the
price rule (batch cost = exact `priceFor(wallet, qty)` on-chain — never
price × qty; a batch straddling the 333 presale boundary mixes presale
and ladder prices).

## X

Official X: **@vanda_nft** — https://x.com/vanda_nft (handle + link only).

## Files

- `index.html` — mint page (PREVIEW state: predicted addresses, mint disabled; hamburger menu, bilingual roadmap, agent-only mint panel)
- `market.html` — marketplace page (PREVIEW state: predicted addresses, no listings, agent-only list/buy/delist)
- `SKILL.md` — agent mint skill
- `llms.txt` — machine-readable summary
- `BRIEF.md` — locked project brief
- `assets/` — hero, emblem, 5 tier images
- `metadata/` — 3,333 extensionless metadata files (IDs 1–3,333)
- `contracts/` — Hardhat project, tests 37/37, CREATE2 predictions

## Disclaimer

NFTs are collectible items and do not promise any return. VANDA is an
independent project on BNB Chain, not a Binance collaboration.
