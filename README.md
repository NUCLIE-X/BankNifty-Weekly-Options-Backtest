# BankNifty-Weekly-Options-Backtest

A Python-based backtesting project that implements a BANKNIFTY weekly ATM straddle strategy with 2% OTM protective wings using historical NSE Futures & Options data.  
This project strictly follows the Quant Research Intern Test Assignment requirements.

---

## 📌 Strategy Summary

This is a rule-based, non-directional options strategy executed once per trading day:

- Sell ATM Call + ATM Put (weekly expiry) at 10:30 AM  
- Buy 2% OTM Call & Put as protective wings  
- Apply 30% Stop Loss and 80% Target (based on straddle premium)  
- Exit all four legs together  
- If SL/Target not hit, exit at 3:20 PM on expiry  
- Starting capital: ₹10,00,000  

---

## 📂 Required Input Data Files

### 1️⃣ BANKNIFTY Futures Data  
**File:** `BANKNIFTY_2017_FUTURES.csv`

**Required Columns:**
- Ticker  
- Date  
- Time  
- Open  
- High  
- Low  
- Close  
- Volume  
- OI  
- Contract  
- Expiry  

**Usage:**
- Futures price at or after 10:30 AM is used to determine the ATM strike  
- Futures are not traded, only used as reference  

---

### 2️⃣ BANKNIFTY Options Data  
**File:** `BANKNIFTY_2017_OPTIONS.csv`

**Required Columns:**
- Ticker  
- Date  
- Time  
- Open  
- High  
- Low  
- Close  
- Volume  
- OI  
- Type (CE / PE)  
- Strike  
- Expiry  
- Contract_Weekly  
- Contract_Monthly  

**Rules Applied:**
- Only weekly contracts are used (Contract_Weekly == "I")  
- Monthly contracts are ignored  

---

## ⚙️ Working Approach

1. Combine Date and Time into Datetime and sort chronologically  
2. Filter weekly options only for efficiency  
3. At 10:30 AM, calculate ATM strike using futures price  
4. Enter 4-leg position (ATM CE, ATM PE, 2% OTM CE, 2% OTM PE)  
5. Monitor position for stop-loss or target  
6. Exit all legs together or at expiry (3:20 PM)  
7. Update capital and record trade details  

---

## 📊 Generated Outputs

### 📈 Graphs
- EquityCurve.png — capital progression over time  
- Drawdown.png — peak-to-trough drawdowns  

### 📑 Reports
- TradeReport.csv — detailed per-trade execution and PnL  
- PerformanceStats.csv — summary metrics (ROI, win rate, drawdown, etc.)

---

## 🧪 Libraries Used

All dependencies are listed in `requirements.txt`:

pandas  
matplotlib  

---

## ✅ Assignment Compliance Checklist

- ATM weekly straddle at 10:30 AM  
- 2% OTM protective wings included in PnL  
- 30% Stop Loss and 80% Target  
- Expiry exit at 3:20 PM  
- Capital starts at ₹10,00,000  
- Trade report generated  
- Performance stats generated  
- Equity curve and drawdown plotted  

---

## 📝 Notes

- Deterministic, rule-based backtest  
- No discretionary assumptions  
- Handles real NSE intraday data issues (missing ticks, liquidity gaps)  
- Designed for large datasets (~585MB options file)  

---

## 👤 Author

Developed as part of a Quant Research Intern Test Assignment  
GitHub: https://github.com/NUCLIE-X
