# 40-Year Decadal Quantitative Backtest Report (1986 – 2026)
**Mathematical Formulations, Multi-Decade Empirical Results & Tax-Adjusted Performance**

---

## Executive Summary

This report delivers a rigorous 40-year empirical evaluation across **897 US equities** and the broad market benchmark (**S&P 500 Index `^GSPC`**) spanning January 1986 through September 2026 (2,122 weekly trading bars).

All returns, Sharpe ratios, and drawdowns are calculated under continuous multi-decade compounding, realistic execution slippage, and an annual **25% capital gains tax** with multi-year net capital loss carryforward.

---

## 1. Mathematical Performance & Tax Accounting Framework

### 1.1 Annual Capital Gains Tax & Loss Carryforward Model

Let statutory tax rate $\tau = 0.25$. For calendar year $y \in \{1986, 1987, \dots, 2026\}$, let $\mathcal{T}_y$ denote the set of closed round-trip transactions completed during year $y$.

For each trade $k \in \mathcal{T}_y$, the realized dollar profit or loss is:
$$\Pi_k = Q_k \cdot \left( P_{exit, k} - P_{entry, k} \right)$$

The annual gross realized capital gain is:
$$\Omega_y = \sum_{k \in \mathcal{T}_y} \Pi_k$$

Let $\mathcal{L}_{y-1} \ge 0$ denote cumulative net capital losses carried forward from year $y-1$. The net taxable gain for year $y$ is:
$$\Gamma_y = \Omega_y - \mathcal{L}_{y-1}$$

The annual tax liability $\text{Tax}_y$ and updated loss carryforward $\mathcal{L}_y$ follow the piecewise formulation:
$$\text{Tax}_y = \begin{cases} \tau \cdot \Gamma_y & \text{if } \Gamma_y > 0 \\ 0 & \text{if } \Gamma_y \le 0 \end{cases}$$
$$\mathcal{L}_y = \begin{cases} 0 & \text{if } \Gamma_y > 0 \\ |\Gamma_y| & \text{if } \Gamma_y \le 0 \end{cases}$$

At year-end, the cash balance $C_y$ is decremented by $\text{Tax}_y$:
$$C_{y, \text{post-tax}} = C_y - \text{Tax}_y$$

---

### 1.2 Quantitative Return and Risk Formulations

Let $E_t$ denote total portfolio equity at week $t \in [0, T]$, where initial capital $E_0 = \$10,000$.

1. **Compound Annual Growth Rate ($\text{CAGR}$)**:
   Given investment horizon $Y = \frac{t_T - t_0}{365.25}$:
   $$\text{CAGR} = \left( \frac{E_T}{E_0} \right)^{\frac{1}{Y}} - 1$$

2. **Maximum Drawdown ($\text{MDD}$)**:
   Let $H_t = \max_{0 \le s \le t} E_s$ denote the historical high-water mark. Drawdown at week $t$ is:
   $$DD_t = \frac{E_t - H_t}{H_t}$$
   $$\text{MDD} = \min_{0 \le t \le T} DD_t$$

3. **Annualized Sharpe Ratio**:
   Let weekly return $r_t = \frac{E_t - E_{t-1}}{E_{t-1}}$, and annualized risk-free rate $R_f = 0.02$ ($r_{f, \text{weekly}} = \frac{R_f}{52}$):
   $$\text{Sharpe} = \frac{\bar{r} - r_{f, \text{weekly}}}{\sigma_r} \cdot \sqrt{52}$$

4. **Calmar Ratio**:
   $$\text{Calmar} = \frac{\text{CAGR}}{|\text{MDD}|}$$

---

## 2. Decadal Breakdown Across Four Macro Regimes

### Decade 1: 1986 – 1996 (Crash of '87, Post-Crash Recovery & Gulf War)
- **S&P 500 Buy & Hold**: +198.0% return | 11.6% CAGR | **-32.7% MaxDD** | 0.75 Sharpe
- **Apex Alpha 7 Slots**: **+1,623.1% return** | **33.1% CAGR** | **-54.4% MaxDD** | **0.97 Sharpe**
- **Apex Alpha 5 Slots**: +2,017.5% return | 35.8% CAGR | -62.0% MaxDD | 0.99 Sharpe
- **Apex Alpha 3 Slots**: +1,440.3% return | 31.6% CAGR | -74.0% MaxDD | 0.75 Sharpe

### Decade 2: 1996 – 2006 (Dot-Com Mania & 2000–2002 Tech Crash)
- **S&P 500 Buy & Hold**: +101.8% return | 7.3% CAGR | -48.5% MaxDD | 0.48 Sharpe
- **Apex Alpha 7 Slots**: **+954.5% return** | **26.6% CAGR** | **-35.7% MaxDD (Safest)** | **0.94 Sharpe**
- **Apex Alpha 5 Slots**: +1,033.3% return | 27.5% CAGR | -47.5% MaxDD | 0.87 Sharpe
- **Apex Alpha 3 Slots**: +1,304.9% return | 30.3% CAGR | -57.0% MaxDD | 0.81 Sharpe

### Decade 3: 2006 – 2016 (2008 Great Financial Crisis & ZIRP Era)
- **S&P 500 Buy & Hold**: +56.0% return | 4.6% CAGR | -56.4% MaxDD | 0.32 Sharpe
- **Apex Alpha 7 Slots**: **+112.9% return** | **7.9% CAGR** | **-49.5% MaxDD (Outperformed Index)** | **0.45 Sharpe**
- **Apex Alpha 5 Slots**: +131.8% return | 8.8% CAGR | -59.8% MaxDD | 0.46 Sharpe
- **Apex Alpha 3 Slots**: +83.5% return | 6.3% CAGR | -67.7% MaxDD | 0.35 Sharpe

### Decade 4: 2016 – 2026 (Tech Expansion, Covid Flash Crash & AI Cycle)
- **S&P 500 Buy & Hold**: +301.2% return | 13.9% CAGR | -33.8% MaxDD | 0.84 Sharpe
- **Apex Alpha 7 Slots**: **+579.0% return** | **19.7% CAGR** | **-40.5% MaxDD** | **0.79 Sharpe**
- **Apex Alpha 5 Slots**: +479.7% return | 17.9% CAGR | -41.7% MaxDD | 0.70 Sharpe
- **Apex Alpha 3 Slots**: +312.5% return | 14.2% CAGR | -48.8% MaxDD | 0.54 Sharpe

---

## 3. Full 40-Year Continuous Compounding & Tax Audit (1986 – 2026)

The table below presents the continuous 40.7-year performance starting with \$10,000 in January 1986 across 897 stocks, with annual 25% tax deductions:

| Strategy Metric | Profile 1: SMART_EXIT (Production Champion) | Profile 2: OPTUNA_SHIELD (10-Yr Optimization) | Profile 3: MACRO_YIELD (40-Yr Economic Overlay) | S&P 500 Buy & Hold (Benchmark) |
| :--- | :---: | :---: | :---: | :---: |
| **Mechanics** | Top 15 Buffer + Runner Immunity ($\ge 15\%$) | Strict Top 15 Buffer + VIX Inversion De-Risk | Yield Curve Inversion + VIX Fear (>28) | Unhedged Passive Long |
| **Pre-Tax Equity** | **\$34,820,110** | **\$26,108,087** | **\$28,450,230** | \$373,384 |
| **Pre-Tax CAGR** | **22.25%** | **21.35%** | **21.65%** | 9.31% |
| **40-Year Net Equity (After 25% Tax)** | **\$7,050,864 (25x S&P 500)** | **\$5,136,359** | **\$5,620,140** | **\$282,538** |
| **40-Year After-Tax CAGR** | **17.51%** | **16.60%** | **16.92%** | **8.57%** |
| **Total Lifetime Taxes Paid** | \$1,728,532 | \$1,309,600 | \$1,410,200 | \$90,846 (at liquidation) |
| **Total Lifetime Round-Trip Trades** | **1,448 trades (-282 churn cut)** | 1,730 trades | 1,405 trades | 0 trades |
| **Max Drawdown** | **-54.4%** | -54.4% | **-52.1%** | -56.4% |
| **Annualized Sharpe Ratio** | **0.82** | 0.80 | 0.81 | 0.59 |
| **Calmar Ratio (After-Tax)** | **0.32** | 0.31 | **0.32** | 0.15 |

---

## 4. Key Quantitative Insights

1. **The Compounding Power of Runner Immunity**:
   - Granting runner immunity to stocks with unrealized gain $G_j(t) \ge +15\%$ prevents selling multi-baggers on cosmetic rank fluctuations.
   - Over 40 years, this generated **+\$1.91 Million in net after-tax wealth** over standard momentum, while slashing round-trip trades from 1,730 down to 1,448 (-282 trades eliminated).

2. **Tax Drag and Drag Reduction**:
   - High-turnover momentum strategies suffer severe friction under an annual 25% capital gains tax.
   - By holding champions longer, Profile 1 reduces realized taxable events and allows capital to compound uninterrupted at higher pre-tax rates.

3. **Macro Regime Cushion**:
   - The 40-week Macro Regime filter successfully avoided the multi-year grind of the 2000–2002 Dot-Com bust (-48.5% index) and the 2007–2009 Global Financial Crisis (-56.4% index), preserving capital to deploy at market bottoms.
