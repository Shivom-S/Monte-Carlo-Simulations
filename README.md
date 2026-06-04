# Monte Carlo Option Pricing Engine

A from-scratch quantitative finance project that prices European options using Monte Carlo simulation and validates results against the Black-Scholes analytical model.

---

## What it does

| Module | Description |
|--------|-------------|
| **Base pricer** | Prices European call & put options via Monte Carlo simulation under risk-neutral measure |
| **GBM path visualisation** | Simulates and plots stock price paths using Geometric Brownian Motion |
| **Greeks (finite difference)** | Estimates Delta, Gamma, Vega, Theta, Rho by bumping parameters |
| **Put-Call parity** | Verifies C − P = S − Ke^{−rT} holds across all moneyness levels |
| **Convergence analysis** | Shows MC price converging to Black-Scholes as N → 1,000,000 |

---

## Sample output

### GBM simulated paths
![GBM Paths](outputs/1_gbm_paths.png)

### Greeks: MC vs Black-Scholes
![Greeks](outputs/2_greeks.png)

### Put-Call parity verification
![Put-Call Parity](outputs/3_put_call_parity.png)

### Convergence to Black-Scholes
![Convergence](outputs/4_convergence.png)

---

## The math

**Stock price under risk-neutral measure (GBM):**

$$S_T = S_0 \cdot \exp\left[\left(r - \frac{\sigma^2}{2}\right)T + \sigma\sqrt{T} \cdot Z\right], \quad Z \sim \mathcal{N}(0,1)$$

**Option price (discounted expected payoff):**

$$C = e^{-rT} \cdot \mathbb{E}\left[\max(S_T - K,\ 0)\right]$$

**Put-Call parity:**

$$C - P = S_0 - Ke^{-rT}$$

**Standard error (why more simulations help):**

$$\text{SE} = \frac{\sigma_{\text{payoff}}}{\sqrt{N}} \propto \frac{1}{\sqrt{N}}$$

---

## Installation

```bash
git clone https://github.com/Shivom-S/monte-carlo-options.git
cd monte-carlo-simulations
pip install -r requirements.txt
```

---

## Usage

**As a notebook:**
Open `monte-carlo-simulations.ipynb` and run all cells. Plots render inline.

Output PNGs are saved to the parent folder.

---

## Default parameters

```python
S0    = 100      # current stock price
K     = 105      # strike price (slightly OTM)
r     = 0.05     # annual risk-free rate (5%)
sigma = 0.20     # annual volatility (20%)
T     = 1.0      # time to expiry (1 year)
N     = 200_000  # number of Monte Carlo simulations
```

All parameters can be changed at the top of `main()`.

---

## Requirements

```
numpy
scipy
matplotlib
```

Or install via:
```bash
pip install -r requirements.txt
```

---

## Results

With default parameters (S=100, K=105, r=5%, σ=20%, T=1yr, N=200,000):

| | Price | Std Error |
|--|-------|-----------|
| **Monte Carlo** | $8.04 | ±0.03 |
| **Black-Scholes** | $8.02 | — |
| **Difference** | $0.02 | — |

Greeks match Black-Scholes to 4 decimal places. Put-Call parity error < $0.01.

---

## Key concepts demonstrated

- **Geometric Brownian Motion** — the standard model for stock price dynamics
- **Risk-neutral valuation** — pricing under the risk-neutral measure using rate `r`
- **Law of Large Numbers** — MC price converges to the true price as N → ∞
- **Central Limit Theorem** — standard error decays as 1/√N
- **Finite difference methods** — numerical differentiation to estimate sensitivities
- **No-arbitrage pricing** — Put-Call parity as a sanity check

---

## Project structure

```
monte-carlo-options/
│
├── monte_carlo_options.py     # main script (all functions + main())
├── monte_carlo_options.ipynb  # Jupyter notebook version
├── requirements.txt
├── README.md
└── outputs/
    ├── 1_gbm_paths.png
    ├── 2_greeks.png
    ├── 3_put_call_parity.png
    └── 4_convergence.png
```

---

## Extensions to explore

- [ ] Antithetic variates / variance reduction techniques
- [ ] Asian options (path-dependent payoffs)
- [ ] American options via Longstaff-Schwartz
- [ ] Implied volatility surface
- [ ] Heston stochastic volatility model
