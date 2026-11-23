# VANDA — Locked Brief

Confirmed by the user 2026-11-23 19:39 WIB. X: user shared
https://x.com/vanda_nft 2026-11-23 20:37 — @vanda_nft is the official
handle (handle + link only; display name / bio / followers unverified).
Presale confirmed 2026-11-23 20:33. Agent-only mint (no wallet button)
+ hamburger menu + bilingual roadmap + market.html ordered 2026-11-23
20:38–20:40.

## Identity

- **Name:** VANDA
- **NFT symbol:** VANDA
- **Token:** $VANDA
- **Tagline:** "It blooms through stone."
- **Language:** English only
- **Chain:** BNB Smart Chain (BSC mainnet), BEP-721
- **Canonical domain:** vanda-five.vercel.app (Vercel project "vanda")
- **GitHub repo:** akungamesatu6-crypto/Vanda (created 2026-11-23)
- **baseURI:** https://vanda-five.vercel.app/metadata/

## Inspiration (reference only — never copy)

A Robinhood Chain VANDA NFT teaser screenshot ("It blooms through stone",
Vanda Miss Joaquim hybrid 1893, 3,333 specimens). The Robinhood project
itself was NOT found on web/IG/Threads — no official site, X, or OpenSea
page located. This is a Binance (BSC) version built from the idea, with
original artwork. Never present it as the Robinhood project or as a
collaboration with it.

## Supply & rarity (sequential)

- **Supply:** 3,333. Token IDs sequential 1–3,333 in mint order, displayed
  as "Accession Nº 001–3,333". Variety follows the ID range — no random
  draw, no reveal.

| Tier | Variety | Range | Count | Share |
|---|---|---|---|---|
| Common | Vanda Alba | 1–1,666 | 1,666 | 50.0% |
| Uncommon | Vanda Rosea | 1,667–2,499 | 833 | 25.0% |
| Rare | Vanda Coerulea | 2,500–2,999 | 500 | 15.0% |
| Epic | Vanda Aurea | 3,000–3,249 | 250 | 7.5% |
| Legendary | Miss Joaquim | 3,250–3,333 | 84 | 2.5% |

## Economics

- **Presale:** first 333 PAID mints cost a flat **0.0001 BNB**. The free
  mint (#1/wallet) still runs during the presale; `presaleSold` counts
  PAID mints only and the presale closes itself at 333 — no owner flip,
  no allowlist. A batch straddling the 333 boundary mixes presale and
  ladder prices.
- **Price ladder (per wallet, cumulative, after the presale):** #1 FREE,
  #2 0.0005, #3 0.001, #4 0.002, #5 0.003, #6 0.005 BNB. **Max 6/wallet.
  Max 0.0115 BNB/wallet.**
- **Gate:** ALL mints via SPACE ID Agent ID; free = any Agent ID holder,
  NO allowlist.
- **Batch:** one `mint(uint256 qty)` transaction; cost = ladder sum of the
  next prices (fresh wallet qty 2 = 0.0005 BNB; fresh wallet qty 6 =
  0.0115 BNB).
- **$VANDA:** 1,000,000,000 total (540,000,000 pool / 460,000,000 treasury);
  **120,000 per PAID mint only** (free mint accrues 0); **max 600,000
  accrued/wallet**.
- **Royalty:** 5% → 0x7379CA652f68fd1daAc11b7b87bb6B222fD129fa.
- **Marketplace:** own escrow, **0% fee** (seller 95% / royalty 5%).
- **Owner / treasury:** 0x7379CA652f68fd1daAc11b7b87bb6B222fD129fa (new wallet).

## Contracts (predicted — CREATE2, salt 0; tests 37/37)

- VandaToken: 0xF4390D14A2B599833e19b135cE9aD3Ae5Db4AECe
- VandaNFT: 0x0C4E3e87eB1194706822Cc7074B4c229F1da0419 (NEW — old 0x30A5… VOID, presale build)
- VandaMarketplace: 0x5b6D7F4D89262a025ffdBd518e37FEF37316dd28 (NEW — old 0x4F35… VOID)
- SPACE ID Agent ID registry: 0x60B9262456dE011F7d15a54CdD8c48bAaa8B022F
- Interim token owner at deploy: 0x05f63E20097c9360D9D68277b90b4a8A8cF8D7C1
- Deploy order: token → NFT → market, all from the paired wallet
  0x05f63E20097c9360D9D68277b90b4a8A8cF8D7C1. Wiring: `setMinter(NFT)`
  once + `transferOwnership(new wallet)`. Mint opens at deploy.
  Est. deploy gas 4,094,151 ≈ 0.0002047 BNB @ 0.05 gwei.
- Full record: `contracts/vanda_predictions.md`

## Artwork (done — Tania-generated, original)

- `assets/hero.jpg` (1040×2272) — Legendary Miss Joaquim + page hero
- `assets/emblem.jpg` (1600×1600)
- `assets/tier-common.jpg`, `tier-uncommon.jpg`, `tier-rare.jpg`,
  `tier-epic.jpg` (Legendary reuses hero.jpg)
- Metadata: 3,333 extensionless files in `metadata/` (IDs 1–3,333)

## Page

- `index.html` — dark botanical-lab design (near-black green, neon-green
  accent, purple orchid accents), mobile-first, EN only, UTC times.
- **PREVIEW state:** zero-address placeholders, mint disabled, PREVIEW
  banner, planned numbers only. Flip at deploy.
- Sections: hero, live status (incl. presale sold / presale state),
  how-it-works, swipe gallery, rarity + table, Legendary feature,
  ROADMAP (bilingual EN + ZH, 4 phases: Presale Opens / Public Mint /
  Full Bloom / Beyond the Bloom — planned, no dates, no return promises),
  mint panel (AGENT-ONLY: qty 1–6, presale-aware total, read-only wallet
  lookup, Agent ID checker, presale-aware agent prompt copy — NO wallet
  connect button, NO browser transaction code), token, marketplace
  (links to market.html), FAQ, contracts, footer/share, sticky-header
  Mint button, fixed bottom dock (both scroll to the mint panel only),
  hamburger menu (Mint / How It Works / Gallery / Rarity / Roadmap /
  Token / Marketplace / FAQ).
- `market.html` — standalone marketplace page: escrow listing live,
  list / buy / delist via agent prompts, read-only listing lookup,
  NO wallet connect, EN only, PREVIEW (no fake listings).

## X / social

- **Official X: @vanda_nft — https://x.com/vanda_nft** (user-shared
  2026-11-23 20:37). Handle + link ONLY on the page and in docs — do NOT
  invent a display name, bio, or follower count. No other social links
  anywhere.

## Standing rules applied

- Completeness first: full page from the start, no stub mint button.
- No Vercel/GitHub mentions on the page. No sellout-total figure. No
  promised returns. No invented links, counts, deadlines, or testimonials.
- Mint-open times in UTC. Independent project — NOT a Binance collaboration.
