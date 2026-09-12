# alpha_trade
Interactive Brokers (IBKR) Apex Alpha Automated Trading System


# **Apex Alpha Trading Algorithm Specification**

## **1\. Executive Summary & Core Mechanics**

The **Apex Alpha Automated Trading Strategy** is a quantitative momentum, multi-cap equity strategy designed for US Equities across the S\&P 1500 universe (covering Large-Cap, Mid-Cap, and Small-Cap stocks with a market capitalization baseline down to $500M) \[cite: 1, 2\].  
The algorithm combines structural Stage 2 trend identification, volume-weighted institutional accumulation, multi-factor momentum acceleration, and real-time SEC Form 4 insider conviction metrics to systematically select, size, and protect positions \[cite: 1, 2\].

## **2\. Complete Algorithm Workflow**

### **Phase 1: Macro Market Regime Filter (SPY Shield)**

Before evaluating individual securities, the algorithm measures overall broad market health using the benchmark index (SPY) \[cite: 1, 2\]:

> * **Calculation:** Evaluates current price relative to its 200-day Simple Moving Average (SMA) \[cite: 1, 2\].  
> * **Bullish Regime (SPY \> 200-day SMA):** Strategy is fully active; capital allocation and regular rebalancing are authorized \[cite: 1, 2\].  
> * **Bearish Regime (SPY \< 200-day SMA):** Triggers an emergency hard sweep into 100% Cash / short-term Treasury ETFs (e.g., SGOV) \[cite: 1, 2\]. All active long equity positions are immediately liquidated to prevent severe drawdowns \[cite: 1, 2\].

### **Phase 2: Stage 2 Golden Filter Gates (Hard Exclusions)**

Every ticker in the candidate universe (\~1,500 liquid stocks down to $500M market cap) must strictly satisfy all five mandatory breakout criteria \[cite: 1, 2\]:

> 1. **Price & Liquidity Minimums:** Price \>= $5.00 and 10-day Average Daily Volume \>= 50,000 shares \[cite: 1, 2\].  
> 2. **Moving Average Alignment:** Price \> 50-day SMA \> 200-day SMA (confirms an established Stage 2 uptrend) \[cite: 1, 2\].  
> 3. **Mansfield Relative Strength Index (MRSI):** MRSI vs. SPY over a 52-week rolling baseline must be \> 0.0 (ensures outperformance relative to the benchmark) \[cite: 1, 2\].  
> 4. **Money Flow Index (MFI):** 14-period MFI \>= 50.0 (confirms underlying institutional volume accumulation) \[cite: 1, 2\].  
> 5. **12-Week Momentum (ROC12W):** 12-Week Rate of Change \> 0.0% \[cite: 1, 2\].

### **Phase 3: Multi-Factor Acceleration Scoring Formula**

Candidates passing all mandatory filters are evaluated and scored using a composite multi-factor formula that measures momentum velocity, short-term acceleration, relative volume ignition, and insider buying conviction \[cite: 1, 2\]:

#### **1\. Base Score Calculation**

The base quantitative score captures multi-week trend momentum, rate-of-change momentum acceleration, and volume expansion \[cite: 1, 2\]:  
`Base Score = ROC12W + (0.50 * ΔROC) + (0.20 * min(RVOL, 3.0))`

> * ROC12W: 12-Week Rate of Change percentage \[cite: 1, 2\].  
> * ROC4W: 4-Week Rate of Change percentage \[cite: 1, 2\].  
> * ΔROC: Acceleration delta defined as ROC4W \- (ROC12W / 3.0) \[cite: 1, 2\].  
> * RVOL: Relative Volume Ignition, calculated as current weekly volume divided by the trailing 10-week average volume \[cite: 1, 2\].

#### **2\. SEC Form 4 Insider Conviction & Dumping Filters**

The algorithm queries live SEC Form 4 insider transaction feeds for all qualifying tickers over a trailing 90-day window \[cite: 1, 2\]:

> * **Insider Purchase Boost (+25%):** If C-Suite executives or Directors made open-market purchases (Code 'P'), the composite score is multiplied by **1.25** \[cite: 1, 2\].  
> * **Heavy Insider Dump Exclusion:** If company executives sold more than $50,000,000 worth of shares in the trailing 90 days, the ticker is automatically rejected from consideration regardless of its technical score \[cite: 1, 2\].

`Final Composite Score = Base Score * (1.25 if Trailing 90-Day Open-Market Insider Purchase else 1.0)`

### **Phase 4: Portfolio Allocation & Asymmetric Holding Rules**

The algorithm enforces a strict capital management and position leash structure \[cite: 1, 2\]:

> * **Fixed Slot Allocation:** The portfolio is divided into up to 7 equal slots (14.28% allocation per position based on Net Liquidation Value) \[cite: 1, 2\].  
> * **Champion Holding Buffer (Top 25 Leash):** An existing held position is *not* sold merely because a new ticker achieves a higher score \[cite: 1, 2\]. As long as a held stock remains within the Top 25 candidate ranking, it is retained to minimize unnecessary portfolio turnover \[cite: 1, 2\].  
> * **Rebalance Execution Timing:** Rebalancing runs weekly on Monday mornings at 09:30 AM EST (Market-on-Open auction execution), avoiding Friday options expiration volatility \[cite: 1, 2\].

### **Phase 5: Risk Management & Exit Architecture**

Position exits occur under three distinct conditions \[cite: 1, 2\]:

| Exit Mechanism | Trigger Condition | Action / Schedule   |
| :---- | :---- | :---- |
| **Macro Regime Exit** | SPY closes below its 200-day SMA \[cite: 1, 2\]. | Immediate market exit of all positions to 100% Cash / SGOV \[cite: 1, 2\]. |
| **Individual Structural Breakdown** | Stock closes below its 50-day SMA \[cite: 1, 2\]. | Evaluated daily at 15:50 EST (Emergency Stop Monitor) and exited before close \[cite: 1, 2\]. |
| **Rank Degradation** | Stock drops outside the Top 25 Champion Buffer \[cite: 1, 2\]. | Liquidated during the regular Monday morning rebalance to free capital for higher-ranked candidates \[cite: 1, 2\]. |

## **3\. Summary Parameters Reference**

| Parameter Name | Value | Description   |
| :---- | :---- | :---- |
| MAX\_SLOTS | 7 | Maximum concurrent stock positions (14.28% capital allocation each) \[cite: 1, 2\] |
| CHAMPION\_BUFFER | 25 | Top N rank cutoff to retain active positions without selling \[cite: 1, 2\] |
| INSIDER\_BUY\_BOOST | \+25% (1.25x) | Score multiplier for stocks with recent open-market insider buying \[cite: 1, 2\] |
| MAX\_INSIDER\_DUMP\_VAL | $50,000,000 | Threshold for disqualifying stocks with heavy executive dumping \[cite: 1, 2\] |
| INSIDER\_WINDOW\_DAYS | 90 Days | Trailing window used for SEC Form 4 insider analysis \[cite: 1, 2\] |
| REBALANCE\_SCHEDULE | Monday 09:30 EST | Weekly portfolio ranking and rebalancing execution time \[cite: 1, 2\] |
| DAILY\_STOP\_SCHEDULE | Mon-Fri 15:50 EST | Daily pre-close structural emergency stop monitoring time \[cite: 1, 2\] |
