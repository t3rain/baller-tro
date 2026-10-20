# Optimal Strategy for Balatro

## Motivation

A Balatro blind is a finite-horizon decision problem under uncertainty. The state is
the current hand, the remaining deck, hands left, discards left, and chips still needed
to reach the target, together with a fixed scoring configuration (base chips and mult
per hand type). Jokers, enhancements and boss effects are out of scope for v1.

This project asks two questions:

1. **Decision:** For a given state, what is the probability of clearing the blind under
   each available action (each play or discard), and which action maximizes it?
2. **Measurement:** How much worse do simple heuristic policies perform than near-optimal
   play, and in which states does the gap concentrate?

"Near-optimal" here means a rollout-improved policy that evaluates each action by Monte
Carlo simulation. It is validated against exact combinatorial solutions wherever those
are tractable (single-discard decisions).


## Rules and Assumptions

1. 


