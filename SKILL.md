# VANDA — Agent Mint Skill

> **PREVIEW — contracts NOT deployed yet.** The addresses below are CREATE2
> predictions, staged for deploy. Before minting, verify on BscScan that
> contract code exists at the NFT address. If it has no code, STOP — mint is
> not open yet. The page (`index.html`) is in PREVIEW state: zero-address
> placeholders, mint disabled, planned numbers only.

## Collection

- **Name:** VANDA · **NFT symbol:** VANDA · **Token:** $VANDA
- **Tagline:** "It blooms through stone."
- **Chain:** BNB Smart Chain (BSC mainnet, chain ID 56), BEP-721
- **Supply:** 3,333 — **SEQUENTIAL** token IDs 1–3,333, displayed as
  "Accession Nº 001–3,333". IDs are assigned in mint order; there is no
  random draw and no reveal.
- **Language:** English only. **Canonical domain:** https://vanda-five.vercel.app/
- **baseURI:** https://vanda-five.vercel.app/metadata/
- **Owner / treasury / royalty receiver:**
  `0x7379CA652f68fd1daAc11b7b87bb6B222fD129fa`

## Rarity (sequential ranges — variety follows the Accession number)

| Tier | Variety | Accession Nº | Count | Share |
|---|---|---|---|---|
| Common | Vanda Alba | 001–1,666 | 1,666 | 50.0% |
| Uncommon | Vanda Rosea | 1,667–2,499 | 833 | 25.0% |
| Rare | Vanda Coerulea | 2,500–2,999 | 500 | 15.0% |
| Epic | Vanda Aurea | 3,000–3,249 | 250 | 7.5% |
| Legendary | Miss Joaquim | 3,250–3,333 | 84 | 2.5% |
| **Total** | 5 varieties | 001–3,333 | **3,333** | 100% |

The Legendary Miss Joaquim is the 1893 Singapore hybrid (Vanda hookeriana ×
Vanda teres), Singapore's national flower. Only 84 specimens — the last 84
mints of the collection.

## Presale (first 333 PAID mints @ 0.0001 BNB flat)

- The first 333 **paid** mints cost a flat **0.0001 BNB** each, instead of
  the ladder price. The free mint (#1 per wallet) still runs during the
  presale and never counts toward the 333.
- `presaleSold` counts **paid mints only**; the presale closes itself at
  333 — no owner flip, no allowlist. After it closes, paid mints return
  to the per-wallet ladder.
- A batch may **straddle the boundary**: each mint in the batch is priced
  in order, so a batch can contain presale-priced and ladder-priced
  mints. Fresh wallet, qty 2 during the presale = 0 + 0.0001 =
  **0.0001 BNB**. At presaleSold = 332, a fresh wallet minting 3 paid
  (batch of 4 incl. free) pays 0 + 0.0001 + 0.001 + 0.002.
- Always read the exact batch cost from `priceFor(wallet, qty)` on-chain
  — never compute it locally, never use price × qty.

## Price ladder (ALL mints via SPACE ID Agent ID; free = any Agent ID holder, NO allowlist; applies to paid mints AFTER the presale)

| Mint # (per wallet, cumulative) | Price |
|---|---|
| #1 | FREE |
| #2 | 0.0005 BNB |
| #3 | 0.001 BNB |
| #4 | 0.002 BNB |
| #5 | 0.003 BNB |
| #6 | 0.005 BNB |

- **Max 6 per wallet** (1 free + 5 paid). **Max 0.0115 BNB per wallet.**
- After the presale, a batch costs the **ladder sum** of the next prices
  — NEVER price × qty. Fresh wallet, qty 2 = 0 + 0.0005 = **0.0005 BNB**.
  Fresh wallet, qty 6 = **0.0115 BNB**. Wallet with 1 mint, qty 2 =
  0.0005 + 0.001 = **0.0015 BNB**.
- Minting is one transaction: `mint(uint256 qty)` mints the next sequential
  IDs and charges the exact `priceFor(wallet, qty)`. The exact value comes
  from `priceFor(wallet, qty)` read on-chain — always use that value, never
  a locally computed one, when sending the transaction.

## Minting is agent-only

There is NO wallet button on the page and NO browser transaction code.
The page only reads public on-chain data (live stats, Agent ID checker,
read-only wallet lookup) and hands the user copyable agent prompts. The
agent calls `mint()` / `mint(uint256)` directly after the user confirms.

## $VANDA token

- **Total supply:** 1,000,000,000 (1B) — **540,000,000 bonus pool /
  460,000,000 treasury**.
- **Bonus:** **120,000 $VANDA per PAID mint only** (free mint accrues 0).
- **Cap:** **600,000 $VANDA accrued per wallet** (5 paid mints).
- **Royalty:** 5% to the owner on secondary sales.
- **Marketplace:** own escrow, **0% fee** — seller receives 95%, royalty 5%.

## Contracts (PREDICTED — CREATE2, salt 0, deploy order token → NFT → market)

| Contract | Predicted address |
|---|---|
| VandaToken ($VANDA) | `0xF4390D14A2B599833e19b135cE9aD3Ae5Db4AECe` |
| VandaNFT (VANDA) | `0x0C4E3e87eB1194706822Cc7074B4c229F1da0419` |
| VandaMarketplace | `0x5b6D7F4D89262a025ffdBd518e37FEF37316dd28` |

- **SPACE ID Agent ID registry (BSC mainnet):**
  `0x60B9262456dE011F7d15a54CdD8c48bAaa8B022F`
- **Interim token owner at deploy (paired wallet):**
  `0x05f63E20097c9360D9D68277b90b4a8A8cF8D7C1`
- Full prediction record: `contracts/vanda_predictions.md`
- **Mint opens AT DEPLOY** (`mintOpen = true` in the constructor).

## Deploy + wiring order (REQUIRED — paid minting reverts without it)

Deploy from the paired wallet `0x05f63E20097c9360D9D68277b90b4a8A8cF8D7C1`.
Est. total gas 4,094,151 ≈ 0.0002047 BNB @ 0.05 gwei.

1. Deploy `VandaToken` (owner at deploy = interim paired wallet).
2. Deploy `VandaNFT`.
3. Deploy `VandaMarketplace`.
4. Interim token owner calls `setMinter(NFT)` on the token — **ONCE, never
   again** (setMinter REPLACES the minter; a second call breaks bonus accrual).
5. Interim token owner calls `transferOwnership(0x7379CA652f68fd1daAc11b7b87bb6B222fD129fa)`
   on the token.
6. Verify on BscScan: token owner = new wallet, `minter()` = NFT address,
   token balance of new wallet = 1,000,000,000 VANDA, NFT owner = new wallet,
   marketplace owner = new wallet, NFT `mintOpen` = true, `totalMinted` = 0.
7. Flip the page: replace the zero-address placeholders with the deployed
   addresses, remove the PREVIEW banner, re-verify the live page.

## Selectors (verified against compiled artifacts)

- NFT: `totalMinted()` `0xa2309ff8` · `paidMinted()` `0x2806b8fb` ·
  `freeMinted()` `0xd10a1a2b` · `mintOpen()` `0x24bbd049` ·
  `presaleSold()` `0x48cebd67` · `presaleActive()` `0x53135ca0` ·
  `MAX_SUPPLY()` `0x32cb6b0c` · `mintedOf(address)` `0x617692dd` ·
  `priceFor(address)` `0xf12a7add` ·
  `priceFor(address,uint256)` `0xd527979a` · `mint(uint256)` `0xa0712d68` ·
  `mint()` `0x1249c58b`
- Token: `accruedOf(address)` `0xea0c88b2` · `balanceOf(address)` `0x70a08231`
- Registry: `balanceOf(address)` `0x70a08231`
- Marketplace: `listing(uint256)` `0x84a184de` (returns seller, price,
  active) · `list(uint256,uint256)` `0x50fd7367` ·
  `buy(uint256)` `0xd96a094a` · `delist(uint256)` `0x964bc33f` ·
  `updatePrice(uint256,uint256)` `0x82367b2d`

## Agent prompt — free mint

> You are my minting agent for the VANDA NFT collection on BNB Chain (BSC
> mainnet, chain ID 56).
>
> NFT CONTRACT (PREDICTED — verify on BscScan that contract code exists
> before minting; if it has no code yet, STOP):
> `0x0C4E3e87eB1194706822Cc7074B4c229F1da0419`
>
> COLLECTION: VANDA — 3,333 supply, BEP-721, SEQUENTIAL token IDs 1–3,333
> ("Accession Nº 001–3,333"). PRESALE: the first 333 PAID mints cost a
> flat 0.0001 BNB; the free mint still runs during the presale.
> `presaleSold` counts PAID mints only; the presale closes itself at 333.
> PRICE LADDER (per wallet, after the presale): #1 FREE, #2 0.0005,
> #3 0.001, #4 0.002, #5 0.003, #6 0.005 BNB. Max 6 per wallet.
> GATE: every mint requires a SPACE ID Agent ID. Registry:
> `0x60B9262456dE011F7d15a54CdD8c48bAaa8B022F` — check `balanceOf(MY_WALLET)`
> > 0 first; if 0, STOP.
>
> Before minting, you MUST call these read-only functions and report the
> exact results: 1. `mintOpen()` — if false, STOP. 2. `totalMinted()` —
> current count and remaining supply. 3. `presaleActive()` and
> `presaleSold()` — presale status. 4. `mintedOf(MY_WALLET)` — if already
> 6, STOP. 5. `priceFor(MY_WALLET, 1)` — exact cost of my next mint; for a
> free mint it must be 0.
>
> Then ask me to confirm. Only after confirmation, call `mint(1)` and send
> exactly `priceFor(MY_WALLET, 1)` in BNB (0 for the free mint). Do NOT
> approve any token spending — this mint is paid in native BNB only. After
> the transaction, report the transaction hash and the new Accession number.

## Agent prompt — paid / batch mint

> You are my minting agent for the VANDA NFT collection on BNB Chain (BSC
> mainnet, chain ID 56).
>
> NFT CONTRACT (PREDICTED — verify on BscScan that contract code exists
> before minting; if it has no code yet, STOP):
> `0x0C4E3e87eB1194706822Cc7074B4c229F1da0419`
> TOKEN CONTRACT (PREDICTED): `0xF4390D14A2B599833e19b135cE9aD3Ae5Db4AECe`
> ($VANDA)
>
> COLLECTION: VANDA — 3,333 supply, BEP-721, SEQUENTIAL token IDs 1–3,333
> ("Accession Nº 001–3,333"). PRESALE: the first 333 PAID mints cost a
> flat 0.0001 BNB; the free mint still runs during the presale.
> `presaleSold` counts PAID mints only; the presale closes itself at 333.
> A batch straddling the boundary mixes presale and ladder prices.
> PRICE LADDER (per wallet, after the presale): #1 FREE, #2 0.0005,
> #3 0.001, #4 0.002, #5 0.003, #6 0.005 BNB. Max 6 per wallet, max 0.0115
> BNB per wallet. BONUS: each PAID mint accrues 120,000 $VANDA (max 600,000
> per wallet). Free mint accrues 0. Presale paid mints accrue the same
> 120,000. GATE: every mint requires a SPACE ID Agent ID. Registry:
> `0x60B9262456dE011F7d15a54CdD8c48bAaa8B022F` — check
> `balanceOf(MY_WALLET)` > 0 first; if 0, STOP.
>
> Before minting, you MUST call these read-only functions and report the
> exact results: 1. `mintOpen()` — if false, STOP. 2. `totalMinted()` —
> current count and remaining supply. 3. `presaleActive()` and
> `presaleSold()` — presale status; a batch near 333 may straddle the
> boundary. 4. `mintedOf(MY_WALLET)` — how many I already minted; my batch
> must fit in 6 minus that number.
> 5. `priceFor(MY_WALLET, QUANTITY)` — exact cost of the batch.
> NEVER use price x quantity — the presale flat price and the ladder make
> that wrong.
>
> Then ask me to confirm the quantity (1–6 minus what I already minted).
> Only after confirmation, call `mint(QUANTITY)` in ONE transaction and send
> exactly `priceFor(MY_WALLET, QUANTITY)` in BNB. Do NOT approve any token
> spending — this mint is paid in native BNB only. After the transaction,
> report the transaction hash and the new Accession numbers.

## Marketplace agent prompts (`market.html`, agent-only, no wallet button)

Marketplace `0x5b6D7F4D89262a025ffdBd518e37FEF37316dd28` (PREDICTED).
Escrow model: `list()` moves the NFT into the marketplace; `delist()`
returns it; `buy()` pays the exact listed price — seller 95%, royalty 5%,
marketplace fee 0%. No floor price.

- **List:** verify `ownerOf(TOKEN_ID)` = MY_WALLET and `listing(TOKEN_ID)`
  not active; approve the marketplace (`approve` / `setApprovalForAll`);
  call `list(TOKEN_ID, PRICE_IN_WEI)` with price > 0.
- **Buy:** read `listing(TOKEN_ID)` (seller, price, active); if not
  active, STOP; call `buy(TOKEN_ID)` sending EXACTLY the listed price in
  BNB, native BNB only.
- **Delist / reprice:** read `listing(TOKEN_ID)`; seller must be
  MY_WALLET; call `delist(TOKEN_ID)` or `updatePrice(TOKEN_ID,
  NEW_PRICE_IN_WEI)` (price > 0).
- Full copyable prompts live on `market.html`.

## X (social)

- **Official X: @vanda_nfth — https://x.com/vanda_nfth** (handle + link
  only; no display name, bio, or follower count invented).

## Honesty rules

- VANDA is an independent project on BNB Chain, NOT a Binance collaboration.
- Never invent a minted count, deadline, collaboration, or testimonial.
- Token IDs are sequential in mint order — say so plainly; there is no
  random draw.
