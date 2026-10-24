## v1 Rules

### Overview

A blind is a single-player game against a shuffled deck. The player has a limited number
of hands and discards to reach a chip target. v1 models one blind in isolation, with a
standard deck and no jokers or other modifiers.

### Setup

| Parameter | Value |
|---|---|
| Deck | Standard 52 cards (4 suits × 13 ranks), shuffled at the start of the blind |
| Hand size | 8 cards |
| Hands per blind | 4 |
| Discards per blind | 3 |
| Max cards per action | 5 |
| Chip target | Experiment parameter (see [Targets](#targets)) |

### Actions

On each turn the player selects 1–5 cards from their hand and either:

- **Plays** them: the selected cards are classified as a hand, scored, and added to the
  running total. Uses one hand.
- **Discards** them: the selected cards are removed without scoring. Uses one discard, and
  is only allowed while discards remain.

After either action, the played or discarded cards leave the game, and replacement cards are
drawn from the remaining deck until the hand is back to 8 cards.

### Hand classification

The played cards (1–5) are classified as the highest-ranked hand type they form (see the
table below).

- **Pair, Two Pair, Three of a Kind, Four of a Kind and High Card** can be formed from
  fewer than 5 cards.
- **Straight, Flush, Full House and Straight Flush** require all 5 cards.
- **Aces** can be high (10-J-Q-K-A) or low (A-2-3-4-5) in a straight. Straights do not
  wrap around (Q-K-A-2-3 is not a straight).
- A **Royal Flush** is scored as a Straight Flush.

### Scoring

Score = (base chips + chips of scoring cards) × mult

- **Scoring cards** are only the cards that form the hand. Other played cards (kickers)
  add nothing. For example, 9♠ 9♣ 2♥ 2♠ 4♣ is a Two Pair: the 9s and 2s score, and the
  4♣ does not.
- **Card chips:** 2–10 = face value, J/Q/K = 10, A = 11 (including when played low in a
  straight).
- The scoring table is fixed in v1 (all hands at level 1).

| Hand | Base chips | Mult | In v1? | Example (played cards) | Example score |
|---|---:|---:|:---:|---|---|
| Flush Five | 160 | 16 | ✗ | **A♠ A♠ A♠ A♠ A♠** | (160 + 55) × 16 = **3440** |
| Flush House | 140 | 14 | ✗ | **K♥ K♥ K♥ 7♥ 7♥** | (140 + 44) × 14 = **2576** |
| Five of a Kind | 120 | 12 | ✗ | **9♠ 9♥ 9♦ 9♣ 9♠** | (120 + 45) × 12 = **1980** |
| Straight Flush | 100 | 8 | ✓ | **9♣ 10♣ J♣ Q♣ K♣** | (100 + 49) × 8 = **1192** |
| Four of a Kind | 60 | 7 | ✓ | **Q♠ Q♥ Q♦ Q♣** 3♠ | (60 + 40) × 7 = **700** |
| Full House | 40 | 4 | ✓ | **8♠ 8♥ 8♦ 4♣ 4♠** | (40 + 32) × 4 = **288** |
| Flush | 35 | 4 | ✓ | **2♦ 5♦ 8♦ J♦ K♦** | (35 + 35) × 4 = **280** |
| Straight | 30 | 4 | ✓ | **A♠ 2♥ 3♦ 4♣ 5♠** | (30 + 25) × 4 = **220** |
| Three of a Kind | 30 | 3 | ✓ | **7♠ 7♥ 7♦** K♣ 2♠ | (30 + 21) × 3 = **153** |
| Two Pair | 20 | 2 | ✓ | **J♠ J♥ 4♦ 4♣** 9♠ | (20 + 28) × 2 = **96** |
| Pair | 10 | 2 | ✓ | **A♠ A♥** 9♦ 6♣ 2♠ | (10 + 22) × 2 = **64** |
| High Card | 5 | 1 | ✓ | **K♠** 7♥ 5♦ 3♣ 2♠ | (5 + 10) × 1 = **15** |

Flush Five, Flush House and Five of a Kind need duplicate cards, which only exist in
modified decks, so they cannot occur in v1's standard 52-card deck.

### Blind outcome

- **Cleared:** the running total reaches or exceeds the target. The blind ends immediately.
- **Failed:** all hands are used and the total is still below the target. Unused discards
  are irrelevant.

### Targets

Without jokers, scores are low, so the target is treated as an **experiment parameter**:
results are reported across a grid of targets. Ante-1 values (300 / 450 / 600 for small /
big / boss blind, with boss effects disabled) are used as reference points.

### Deck exhaustion

Unreachable in v1. At most 8 + 6 × 5 = 38 cards are ever drawn: the initial hand plus
refills after up to 6 actions (the blind ends after the 7th). That's fewer than 52. For
robustness, if the deck runs out, the engine draws as many cards as remain and play
continues with a smaller hand.

### Out of scope (v1)

Jokers, hand levels (planet cards), card enhancements, editions, seals, boss blind effects,
tarot/spectral cards, shop and economy, and modified decks.

