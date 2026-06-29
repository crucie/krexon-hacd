# Stack Design: KREXON

## Asset type
**Fungible Token (FT)** — with lot-level identity preserved at the HACD layer

Each HACD lot forms a fixed quantity of KREXON (KRX). On Solana, KRX is fungible and tradeable in AMM pools. On the HACD layer, the formation record of each lot is permanently preserved — giving partners and auditors a traceable origin for every unit in supply.

---

## Supply

| Parameter | Value | Notes |
|---|---|---|
| **Total supply** | 100,000,000 KRX | Needs issuer confirmation |
| **HACD lots** | 1,000 | 1 HACD = 1 lot — Needs issuer confirmation |
| **Units per HACD lot** | 100,000 KRX | Fixed across all lots |
| **All lots equal?** | Yes (default) | Tiered structure possible for partner lots |

**Supply formula verification:**
```
total_supply = total_hacd_lots × units_per_hacd_lot
100,000,000 = 1,000 × 100,000 ✓
```

---

## Stack cost

| Parameter | Value | Notes |
|---|---|---|
| **Stack cost per HACD** | 100 HAC | Needs issuer confirmation |
| **Estimated total formation cost** | 100,000 HAC | At 100 HAC × 1,000 lots |
| **Network fee** | Variable | Check live: explorer.hacash.org |
| **Minimum per participant** | 1 HACD + 100 HAC + network fee | Needs issuer confirmation |

**Formation cost formula:**
```
formation_cost_hac = total_hacd_lots × stack_cost_per_hacd
formation_cost_hac = 1,000 × 100 = 100,000 HAC
```

**Formation reference (not a price floor):**
Each KRX unit has a visible on-chain formation cost reference of:
```
minimum_formation_reference = 1 HACD + 100 HAC + network fee
                              distributed across 100,000 KRX per lot
```
This is a formation cost reference only — not a guaranteed redemption value or price floor.

---

## Formation rules

1. Each Stack lot requires exactly 1 HACD unit as the container
2. The stacker pays 100 HAC as the formation cost (stack cost) per HACD
3. Upon successful Stack transaction, 100,000 KRX are formed and attributed to that HACD lot
4. The HACD + formation record is permanently inscribed on-chain
5. All lots follow identical rules — no preferential pricing (unless a partner tier structure is later confirmed by the issuer)
6. KRX formed on HACD is then eligible for bridge/wrap to Solana for AMM participation

---

## Participant flow

**For individual stackers:**
1. Acquire 1 or more HACD units
2. Prepare 100 HAC per HACD (plus network fee) in a compatible Hacash wallet
3. Navigate to KREXON Launchpad
4. Enter HACD name(s) for the Stack lot(s)
5. Confirm Stack transaction
6. Verify formed KRX on Launchpad and Hacash explorer
7. Bridge or wrap KRX to Solana wallet for DEX participation

**For loyalty program partners (B2B flow):**
1. Partner engagement with KREXON team
2. Designated HACD lot allocation (if partner tier confirmed)
3. Stack formation with KREXON team facilitation
4. KRX attributed to partner's treasury or loyalty program integration
5. Partner provides KRX redemption pathway to their points holders

---

## Two-layer architecture

```
┌─────────────────────────────────────────────────┐
│              HACD LAYER (Hacash)                │
│                                                 │
│  1,000 HACD lots → 100,000,000 KRX formed      │
│  Stack cost: 100 HAC per HACD                   │
│  Formation history: permanent, on-chain          │
│  Provable scarcity: enforced at issuance         │
└────────────────────┬────────────────────────────┘
                     │
              Bridge / Wrap
              (mechanism TBC)
                     │
┌────────────────────▼────────────────────────────┐
│              SOLANA LAYER                        │
│                                                 │
│  KRX circulates as SPL token                    │
│  AMM pools: KRX / loyalty point tokens          │
│  Sub-second finality, near-zero swap fees        │
│  Mobile-friendly UX for non-crypto users         │
└─────────────────────────────────────────────────┘
```

---

## Removal / burn logic

*Needs issuer confirmation.* Recommended default:

- Stack removal (unstacking) disables the KRX formation for that HACD lot
- KRX already in circulation on Solana is unaffected (remains liquid)
- The HACD unit is returned to the stacker
- Formation record remains on-chain permanently (history is immutable)

This approach protects existing KRX holders while giving stackers optionality on their HACD.

---

## Open items requiring issuer confirmation

- [ ] Final total supply and lot count
- [ ] Stack cost per HACD in HAC (100 HAC is a draft assumption)
- [ ] Minimum HACD required per participant
- [ ] Designated address requirement for partner lots
- [ ] Bridge / wrap mechanism to Solana (critical path item)
- [ ] Stack removal / burn behavior
- [ ] Whether partner tiers get preferential lot allocation
