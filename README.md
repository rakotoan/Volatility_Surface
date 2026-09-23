# Implied Volatility Surface

Welcome to the **Implied Volatility Surface** project. This project retrieves listed option data and constructs a three-dimensional implied volatility surface for any asset **options** availabe on Yahoo Finance.

The objective is to transform option-chain quotes into a volatility surface across strikes and maturities, using the Black–Scholes framework and numerical implied-volatility estimation.

---


# ⚙️ Working Conditions

💶 Risk-Free Interest Rate: **\(r = 3\%\)**  
💸 Dividend Yield: **\(q = 0\%\)**  




> **Note:** The option-chain data are retrieved dynamically from Yahoo Finance through the `yfinance` Python package.
---

# 🎯 Goal

The goal is to construct and visualise the implied volatility surface:

$$
\sigma_{\mathrm{imp}} = \sigma_{\mathrm{imp}}(K,T)
$$

where:

- $K$ is the option strike;
- $T$ is time to maturity;
- $\sigma_{\mathrm{imp}}$ is the volatility that matches the Black–Scholes theoretical price to the observed market option price.

---

# 🧠 Methodology

1. **Market Data Collection and Data Preparation**

The project uses `yfinance` to retrieve the latest asset spot price, available expiration dates and call/put option chains. For each contract, key fields such as strike, bid, ask, last price, volume, open interest and implied volatility are collected.

The dataset is filtered to remove missing, zero-priced or unreliable observations.

2. **Implied Volatility Calculation**

For each option contract, implied volatility is obtained by matching the theoretical Black–Scholes option price to the observed market price:

$$
P_{\mathrm{BS}}(\sigma_{\mathrm{imp}}) = P_{\mathrm{market}}
$$

where $P_{\mathrm{market}}$ is the observed option market price and $P_{\mathrm{BS}}(\sigma)$ is the theoretical Black–Scholes option price as a function of volatility.

Since implied volatility cannot be isolated analytically from the Black–Scholes formula, the volatility input is adjusted numerically until the theoretical price matches the observed market price.

3. **Implied-Volatility Surface**

Each valid option contract is characterised by a strike $K$, a time to maturity $T$ and an implied volatility $\sigma_{\mathrm{imp}}$. Together, these observations define the implied-volatility surface:

$$
\sigma_{\mathrm{imp}} = \sigma_{\mathrm{imp}}(K,T)
$$

The surface is analysed through two complementary dimensions:

- **Volatility skew / smile:** for a fixed maturity $T$, implied volatility is observed across different strikes $K$.
- **Volatility term structure:** for a fixed strike $K$, implied volatility is observed across different maturities $T$.


The full volatility surface combines these two dimensions and provides a joint view of implied volatility across strikes and maturities.

---
# 📊 Results

The output is a three-dimensional implied volatility surface.

The black dots correspond to the observed option data used to construct the surface. The coloured surface is obtained through interpolation and should therefore be interpreted cautiously in sparse regions.

> **AI assistance note:** LLM assistance was used specifically for the technical implementation of interpolation and 3D surface visualisation.
---


# ⚙️ Prerequisites

To run this project, ensure that you have:

- 🐍 Python 3
- 📓 Jupyter Notebook
- 📦 Required libraries:
  - `numpy`
  - `pandas`
  - `yfinance`
  - `scipy`
  - `matplotlib`

You can find all dependencies in `requirements.txt`.

---

# 📌 Installation

1. Create and activate a virtual environment:
2. Install the dependencies:

```bash
pip install -r requirements.txt
```

---

# 💻 Usage

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Then open and run:

```text
volatility_surface.ipynb
```

