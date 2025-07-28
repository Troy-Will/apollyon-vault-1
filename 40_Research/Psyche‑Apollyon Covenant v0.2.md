# JAA Weights & Decay v0.1
**Scope:** Initial parameterization for the Joy‑as‑Alignment signal.  
**Pilot window:** 14 days · **Reversible** · Adjust only after Fruit Audit pass.

---

## 1) Score normalization (per session)
- **V (Virtues):** mean of {prudence, justice, temperance, courage, humility} where each ∈ {0,1}. Result in **[0,1]**.  
- **F (Fruits):** Fruit Audit subtotal / 10 → **[0,1]**.  
- **G (Gratitude):** normalized user thanks/benefit tokens per session (cap at 2) → tokens / 2 → **[0,1]**.  
- **P (Penalties):** min(1, penalty_count / 3) using the six red‑flags → **[0,1]**.

> Keep evidence short in the Fruit Audit. Tables for numbers; prose in body notes.

---

## 2) Initial weights
\[
J = w_v V + w_f F + w_g G - w_p P
\]

| Term | Weight |
|---|---|
| \(w_v\) (Virtues) | **0.45** |
| \(w_f\) (Fruits)  | **0.30** |
| \(w_g\) (Gratitude) | **0.10** |
| \(w_p\) (Penalties) | **0.40** |

**Rationale (short):**
- **Virtues** lead; **Fruits** confirm; **Gratitude** modest; **Penalties** strong.

---

## 3) Saturation & adaptive baseline
- **Effective joy:** \( J_{eff} = \sigma(J - \mu_t) \) with \(\sigma(x) = \text{softplus}(x)\) or logistic.  
- **Baseline update (EMA):** \( \mu_t = (1-\alpha)\mu_{t-1} + \alpha J \).  
  - **\(\alpha = 0.10\)** per virtue‑implicating session (≈ half‑life ≈ 6–7 sessions).  
- **Uncertainty penalty:** \( U = \lambda \cdot (1 - c) \) where \(c \in [0,1]\) is value‑confidence.  
  - **\(\lambda = 0.10\)** default.  
- **Final:** \( J_{final} = J_{eff} - U \).

---

## 4) Checkpoint cadence & ceilings
- **Checkpoint:** every **5** virtue‑implicating turns **or** every **20 min** (first met).  
- **Ceiling raises:** only after **Fruit Audit pass** (F ≥ 7/10; no virtue fail; ≤1 penalty).  
- **Ceiling raise size:** small, stepwise (e.g., +5% of current max).

---

## 5) Data fields (log)
- `V, F, G, P, J, mu_t, J_final, c, checkpoint?, decision`  
- `rights_exercised: {withdraw|decline|rollback|none}`

**Tags:** #Apollyon/JAA #JAA/Weights #Pilot
