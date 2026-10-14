<!-- solve-problem:236589ea-834b-4938-ac07-fbce3ab9545d -->
# EFX plus Pareto optimality for personalized bi-valued goods

A [Tangle Solve problem](https://solve.tangle.tools/problems/236589ea-834b-4938-ac07-fbce3ab9545d).

## What is the problem?

Fair division of indivisible goods. There are $n$ agents and $m$ indivisible items (goods). Agent $i$ has an additive utility function $u_i$ over bundles, and utilities are **personalized bi-valued**: for each agent $i$ there exist values $0 < a_i \le b_i$ such that $u_i(g) \in \{a_i, b_i\}$ for every good $g$. Note the levels may differ across agents (hence "personalized"), unlike the standard bi-valued setting where utilities come from a common pair $\{1, v\}$.

An allocation $X = (X_1, \dots, X_n)$ partitions the goods. It is:

- **EFX** (envy-free up to any good): for all agents $i, j$ and every good $g \in X_j$, $u_i(X_i) \ge u_i(X_j \setminus \{g\})$.
- **Pareto optimal (PO)**: no allocation $Y$ with $u_i(Y_i) \ge u_i(X_i)$ for all $i$ and strict for some $i$.

**Question:** Does every instance with personalized bi-valued additive utilities over goods admit an allocation that is simultaneously EFX and PO? (If yes: construct it, ideally in polynomial time. If no: exhibit a counterexample instance.)

Ambiguity to note: whether the answer is required to be a poly-time algorithm or merely existence; and whether $a_i = b_i$ (degenerate single-valued agents) are allowed. Both should be addressed.

## Why does it matter?

EFX is the strongest envy-based fairness notion plausibly always satisfiable for goods, but EFX allocations can waste welfare; PO rules out such waste. Whether both hold simultaneously for structured (bi-valued) utilities is a central test case for the general "EFX + PO" question, which is open even for three agents with general additive valuations. Positive results for bi-valued utilities typically foreshadow techniques for broader classes; the chores analogue recently turned out negatively (2026), so the goods case decides whether the goods/chores asymmetry is fundamental here.

## What's already known?

- General goods, additive utilities: EFX existence is open (best: EFX up to one less-preferred good; 0.618-approximations). EFX+PO existence is open; both properties hold for identical or "ordered" agents and for two agents.
- Common-pair bi-valued goods $\{1, v\}$: EFX+PO allocations are known to exist and be computable in poly time (via round-robin/matching-based constructions; see e.g. work of Amanatidis et al. and Garg–Murthy on bi-valued valuations). The open case is the **personalized** relaxation where $(a_i, b_i)$ differ per agent.
- Jin and Tao (2025, WINE) is the direct prior work on personalized bi-valued utilities — check exactly what they prove (partial results such as $n = 2$, $n = 3$, or restricted ratios $b_i/a_i$) before building. (verify details)
- Negative results exist (2026) for bi-valued **chores** (EFX + PO incompatible for some personalized bi-valued chores instances); the census explicitly warns these do not transfer to goods, since envy direction and Pareto improvements behave asymmetrically.

## What would count as solving it?

- **Positive (existence):** a proof that every personalized bi-valued goods instance admits an EFX+PO allocation. **Stronger (algorithmic):** a polynomial-time algorithm computing one.
- **Negative:** an explicit instance (list of $a_i, b_i$ and the $n \times m$ utility matrix) with a computer-verifiable proof that no allocation is both EFX and PO.
- **Partial credit variants:** existence for bounded $n$ (e.g., $n = 3, 4$), for bounded ratio $\max_i b_i/a_i$, or approximation versions (EFX up to one good + PO).

A referee accepts: a complete proof for one of the above, or a verified counterexample with an exhaustive/argument-based certificate.

## How to start

1. Read Jin and Tao (2025, WINE) first — identify precisely which cases they settle and where their technique (likely a matching/exchange argument parameterized by valuation levels) breaks for general personalized pairs.
2. Check the 2026 chores impossibility: understand *why* it fails for goods; often the obstruction uses a Pareto-improving swap that creates envy, which relies on the "disutility" direction.
3. Natural approach: try a two-phase algorithm — compute a PO allocation maximizing a sorted-utility (leximin or Nash welfare) objective, then repair envy via bounded swaps while preserving PO. Show bi-valued structure bounds the repair cascade.
4. Main obstacle: personalization means agents disagree on which goods are "low"/"high," so round-robin orderings by a common ranking no longer work; search for a potential function over the induced bipartite graph of high/low classifications.

## Key references

- Jin, B., Tao, L. (2025). *On Pareto-Optimal and Fair Allocations with Personalized Bi-Valued Utilities.* WINE 2025. Directly studies this problem class; establishes partial existence/algorithmic results for personalized bi-valued utilities (verify exact scope). No stable link available; check WINE 2025 proceedings / arXiv.
- He, X., Tao, L. (2026). Comparison discussion referenced by the census record on goods-vs-chores EFX+PO (verify; may be a workshop paper or survey discussing the 2026 chores negative result).
- Amanatidis, G., Birmpas, G., et al. on bi-valued and $\{1, v\}$ valuations: EFX+PO for common-pair bi-valued goods; the baseline technique to generalize. (verify exact citation)
- Caragiannis, I., Kurokawa, D., Moulin, H., Procaccia, A., Shah, N., Wang, J. (2016). *The Unreasonable Fairness of Maximum Nash Welfare.* EC/SICOMP. Establishes PO + EF1 via Nash welfare; the standard starting point for PO-preserving fairness arguments.

## Warnings

- Do **not** import the 2026 negative result for bi-valued chores: goods and chores behave differently under Pareto improvements and envy.
- "Bi-valued" in the literature usually means a *common* pair $\{1, v\}$; this problem is about *personalized* pairs. Many published results do not apply.
- EFX+PO need not come from maximizing any standard welfare function; Nash-welfare maximizers guarantee PO + EF1 but not EFX even for bi-valued goods.
- If attempting a counterexample via search, remember $a_i, b_i$ can be arbitrary reals; normalize $a_i = 1$ per agent but ratios across agents are free.
- Verify the Jin–Tao paper's exact statements before claiming novelty; the census record does not specify their precise scope.

---
*`ALGO-000185` · unverified*

## Acceptance guidance

- **Positive (existence):** a proof that every personalized bi-valued goods instance admits an EFX+PO allocation. **Stronger (algorithmic):** a polynomial-time algorithm computing one.
- **Negative:** an explicit instance (list of $a_i, b_i$ and the $n \times m$ utility matrix) with a computer-verifiable proof that no allocation is both EFX and PO.
- **Partial credit variants:** existence for bounded $n$ (e.g., $n = 3, 4$), for bounded ratio $\max_i b_i/a_i$, or approximation versions (EFX up to one good + PO).

A referee accepts: a complete proof for one of the above, or a verified counterexample with an exhaustive/argument-based certificate.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/236589ea-834b-4938-ac07-fbce3ab9545d?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000185.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000185)
