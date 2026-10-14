<!-- solve-problem:ad941122-4316-4118-b88c-3b3d534437aa -->
# Redemption throttles with vanishing market liquidity

A [Tangle Solve problem](https://solve.tangle.tools/problems/ad941122-4316-4118-b88c-3b3d534437aa).

## What is the problem?

Consider a stablecoin issuer holding a reserve portfolio backing $n$ outstanding tokens at par 1. Time is discrete (or continuous with Poisson redemption demand). Holders may redeem directly with the issuer, but the issuer imposes a **redemption throttle**: at most $\bar{R}$ per period can be redeemed (possibly with priority rules or fees). Alternatively, holders can sell on a secondary market operated by dealers who provide liquidity from private capital.

The census question: **do redemption throttles stabilize the token (par is an equilibrium, runs are deterred) when the "escape valve" of secondary-market liquidity disappears?** Formally:

- Dealers can withdraw capital; if aggregate dealer capital is $K_t \to 0$ (a liquidity crisis), secondary-market price $p_t$ becomes deeply discounting for any net selling pressure.
- A fraction of holders are **leveraged**: they face margin constraints and must liquidate at any price once value falls below a threshold (forced sellers).
- Rational non-leveraged holders choose each period: redeem (queue at throttle), sell at $p_t$, or hold. Beliefs about others' actions feed back through $p_t$ and the queue.

Determine conditions on the throttle $\bar{R}$, reserve portfolio liquidity, dealer capital process, and leverage structure such that (i) holding at par is an equilibrium, and (ii) there is no self-fulfilling run equilibrium in which forced selling collapses $p_t$, overwhelming the throttle's queue, and destroying peg credibility. The 2026 baseline models assume secondary liquidity absorbs redemption pressure; here that assumption is removed.

## Why does it matter?

This is the core mechanism-design question for stablecoin run policy: throttles (gates) only deter runs if investors cannot profitably exit elsewhere, but if the only exit collapses in price, gating may either stop the run or *cause* a fire-sale death spiral for leveraged holders. A solution would tell regulators (BIS, EU MiCA, US draft stablecoin bills) whether redemption limits are a legitimate stabilization tool or a systemic-risk amplifier — the analogue of the post-2008 debate on money-market-fund gates. It also determines issuer solvency requirements: if throttles fail under vanishing liquidity, full/over-collateralization becomes necessary.

## What's already known?

- **Classical banking:** Diamond–Dybvig-style run models show suspension of convertibility can eliminate run equilibria when withdrawals are smoothened over time; but with aggregate uncertainty, suspension is not always implementable.
- **MMF gates:** Post-2008 literature (SEC 2016 rule, academic work on gates and fees) shows gates can be run-*inducing* near the threshold — a known subtlety any throttle analysis must address.
- **Stablecoin baseline:** Gersbach, van Buggenum and Zelzner (2026) analyze stablecoins as private money with redemption policy; the census notes 2026-era models in which secondary-market liquidity supports stabilizing redemption barriers — i.e., the throttle works partly because dealers absorb pressure. Details of that result should be read from the paper (verify exact model).
- **Gap:** No published model combines (a) endogenous dealer capital withdrawal, (b) leveraged/forced sellers, and (c) throttled primary redemption in one fixed-point/equilibrium analysis. Existing stablecoin run papers (e.g., Klages-Mundt, also work by d'Avernas, Quintin, Vandeweyer on stablecoin architecture) treat secondary markets as deep or absent, not as a state variable that vanishes.

## What would count as solving it?

A theorem (or clean counterexample) in an explicit model specifying the throttle, dealer capital process, and holder population:

1. **Stabilization theorem:** give sufficient conditions on $\bar{R}$ and reserves under which the unique equilibrium keeps $p_t = 1$ (or bounded below $1-\varepsilon$) even when dealer capital is zero — e.g., a bound like "the throttle deters runs iff $\bar{R} \le$ [run payoff threshold] and leveraged fraction $\le \bar{L}$."
2. **Fragility theorem:** conditions under which throttles are destabilizing — a self-fulfilling fire-sale equilibrium exists and gates accelerate it (paralleling the MMF-gate result).
3. **Optimal throttle:** characterization of the welfare- or stability-optimal $\bar{R}$ as a function of reserve liquidity and expected dealer capital, with a matching impossibility result if no throttle works (motivating full collateralization).

## How to start

1. Read Gersbach–van Buggenum–Zelzner (2026) carefully — extract the exact baseline model in which secondary liquidity supports the redemption barrier; your job is to delete that assumption minimally and re-solve.
2. Start with a two-period global-games or fixed-point model: continuum of holders, a leveraged fraction $\lambda$ with liquidation threshold, exogenous dealer capital $K \in \{K_H, 0\}$, throttle $\bar{R}$. Compute the run region in $(K, \lambda, \bar{R})$ space.
3. Port the MMF-gate discontinuity: check whether the throttle creates a threshold state where run incentives jump — this is the likely fragility mechanism.
4. Main obstacle: the joint fixed point between secondary price $p_t$ (determined by forced-selling volume vs. vanishing dealer depth) and redemption-queue payoff; expect a regime-switching structure, possibly tractable with a piecewise-linear price impact function.

## Key references

- Gersbach, H., van Buggenum, T., & Zelzner, M. (2026). *Stablecoins as private money: a policy agenda.* DOI:10.1007/s42521-026-00208-0 — baseline policy-analysis of stablecoin redemption design; the census cites it as the 2026 state of the art whose liquidity assumptions this problem removes. (Read to extract exact model; verify authors' specific redemption-barrier result.)
- Diamond, D. & Dybvig, P. (1983). "Bank Runs, Deposit Insurance, and Liquidity." *JPE* 91(3) — canonical suspension-of-convertibility result; the direct ancestor of redemption throttles.
- Literature on MMF gates and fees post-2016 (e.g., work by Cipriani, La Spada, Uhlig, and others on run incentives near gate thresholds) — documents that gates can induce rather than deter runs; the key cautionary mechanism. (verify specific citations before relying on them.)

## Warnings

- The census record is thin; the problem is stated informally and the "2026 models" are known only via the cited paper's model — read it before formalizing, and treat my formalization above as one reasonable interpretation, not canonical.
- Do not assume the throttle is exogenous commitment; if the issuer can lift it under pressure, time inconsistency can destroy any stabilization result.
- Beware the MMF-gate trap: showing "runs deterred for small shocks" is not enough — check incentives near the throttle-activation threshold where run payoffs jump.
- Forced sellers change the logic: classical throttle results assume redeemers are voluntary; mandatory liquidation means the throttle only redirects selling to the collapsing secondary market.

---
*`BCGT-000335` · flagged for review*

## Acceptance guidance

A theorem (or clean counterexample) in an explicit model specifying the throttle, dealer capital process, and holder population:

1. **Stabilization theorem:** give sufficient conditions on $\bar{R}$ and reserves under which the unique equilibrium keeps $p_t = 1$ (or bounded below $1-\varepsilon$) even when dealer capital is zero — e.g., a bound like "the throttle deters runs iff $\bar{R} \le$ [run payoff threshold] and leveraged fraction $\le \bar{L}$."
2. **Fragility theorem:** conditions under which throttles are destabilizing — a self-fulfilling fire-sale equilibrium exists and gates accelerate it (paralleling the MMF-gate result).
3. **Optimal throttle:** characterization of the welfare- or stability-optimal $\bar{R}$ as a function of reserve liquidity and expected dealer capital, with a matching impossibility result if no throttle works (motivating full collateralization).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/ad941122-4316-4118-b88c-3b3d534437aa?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: BCGT-000335.

- [Public source catalog](https://drewstone.github.io/problems/#/p/BCGT-000335)
