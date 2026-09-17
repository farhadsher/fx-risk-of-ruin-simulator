# FX Risk of Ruin Simulator Pro

A free Monte Carlo simulator that shows the real range of outcomes for a trading strategy - not just the average. Run it from a theoretical win rate and reward:risk ratio, or bootstrap it straight from your own real trade history, and it runs thousands of simulated trade sequences to show your probability of ruin, Kelly-optimal position size, drawdown risk, and the full distribution of outcomes.

**[Live tool -->](index.html)** (open in any browser, no signup, no server)

Built and maintained by [FXMARE](https://fxmare.com) - forex news, market analysis, and free trading tools.

## Why this exists

Most traders think about their edge as a single average outcome: "I win 45% of the time with a 2:1 reward, so I should be profitable." That is true on average, but it hides the variance. The same strategy can look very different depending on how much you risk per trade - too much risk and a real edge can still have a meaningful chance of blowing the account through a bad losing streak. This tool makes that variance visible, and goes further than a basic simulator by modeling trading costs, streakiness, and your own historical results.

## Features

**Two simulation modes**
- Theoretical mode - set a win rate, reward:risk ratio, and an optional streakiness/correlation parameter (real results are not always independent trade to trade)
- Bootstrap mode - paste your own closed trades as R-multiples and the simulator resamples directly from your real historical distribution instead of a theoretical curve

**Realistic modeling**
- Fixed-fractional position sizing on current balance
- Trading costs (spread, commission, slippage) modeled as a percent of risk per trade
- Optional trade-to-trade correlation (momentum or mean-reversion) instead of assuming pure independence

**Position sizing analysis**
- Kelly criterion calculator (closed-form in theoretical mode, numerically optimized from your data in bootstrap mode)
- Shows your current risk per trade as a multiple of Kelly-optimal sizing, with a plain-language read on whether you're over- or under-betting

**Risk analytics**
- Risk of ruin, probability of profit, median/10th/90th percentile outcomes
- Value at Risk (5%) and Conditional VaR (5%)
- Median and worst-case (90th percentile) max drawdown
- Median and worst-case longest losing streak
- Ulcer Index (a blended depth-and-duration drawdown score)
- A risk % sensitivity table showing how ruin probability and outcomes change at 0.5x-3x your current risk per trade

**Visuals**
- Percentile fan chart of the equity curve (10th/25th/median/75th/90th)
- Percentile fan chart of the drawdown curve
- Histogram of final account balances
- Histogram of max drawdown across all simulated runs

**Everything else**
- Optional seed locking for reproducible comparisons between runs
- Export full results (summary stats + every simulated final balance) as CSV
- Everything computed and rendered client-side - no backend, no tracking, no data leaves your browser (including anything you paste into the trade history box)

## How it works

For each simulated run, every trade risks a fixed percentage of the *current* account balance. In theoretical mode, a win adds `risk x reward:risk ratio` and a loss subtracts the risk amount, minus trading costs either way; in bootstrap mode, each trade's outcome (in R-multiples) is randomly resampled with replacement from the trade history you provide. This is repeated for the chosen number of trades, across as many independent simulations as you set, and the spread of outcomes across all simulations is what gets charted and summarized.

```
Risk amount   = Current balance x Risk %
Trade result  = Risk amount x (R-multiple - trading cost %)
Risk of ruin  = % of simulated runs where balance fell to the ruin threshold
Kelly f*      = (p*w - q*L) / (w*L)   for win probability p, win multiple w, loss multiple L
```

## Usage

This is a single self-contained HTML file - no dependencies, no build tools, no tracking.

- Open `index.html` directly in a browser, or
- Serve it with any static file host.

## Disclaimer

This tool is for educational purposes only and does not constitute financial advice. Simulated results depend heavily on the simplifying assumptions you choose (independent or correlated trades, a fixed cost assumption, resampling from a limited trade history); real markets and real execution can differ. Past or simulated performance does not guarantee future results.

## License

MIT - see [LICENSE](LICENSE).
