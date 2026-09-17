# FX Risk of Ruin Simulator

A free Monte Carlo simulator that shows the real range of outcomes for a trading strategy - not just the average. Enter your win rate, reward:risk ratio, and risk per trade, and it runs thousands of simulated trade sequences to show your probability of ruin, a percentile fan chart of possible equity curves, and the distribution of final outcomes.

**[Live tool -->](index.html)** (open in any browser, no signup, no server)

Built and maintained by [FXMARE](https://fxmare.com) - forex news, market analysis, and free trading tools.

## Why this exists

Most traders think about their edge as a single average outcome: "I win 45% of the time with a 2:1 reward, so I should be profitable." That is true on average, but it hides the variance. The same strategy can look very different depending on how much you risk per trade - too much risk and a real edge can still have a meaningful chance of blowing the account through a bad losing streak. This tool makes that variance visible instead of hidden inside a single expected-value number.

## Features

- Adjustable starting balance, risk per trade, win rate, reward:risk ratio, trade count, number of simulations, and ruin threshold
- Monte Carlo engine runs thousands of independent simulated trade sequences with fixed-fractional position sizing
- Risk of ruin, probability of profit, median outcome, and 10th/90th percentile outcomes
- Percentile fan chart of the equity curve (10th, 25th, median, 75th, 90th)
- Histogram of the distribution of final account balances
- Everything computed and rendered client-side - no backend, no tracking, no data leaves your browser

## How it works

For each simulated run, every trade risks a fixed percentage of the *current* account balance. A win adds `risk x reward:risk ratio`; a loss subtracts the risk amount. This is repeated for the chosen number of trades, across as many independent simulations as you set, and the spread of outcomes across all simulations is what gets charted.

```
Risk amount   = Current balance x Risk %
Trade result  = +Risk amount x Reward:Risk   (win)
              = -Risk amount                 (loss)
Risk of ruin  = % of simulated runs where balance fell to the ruin threshold
```

## Usage

This is a single self-contained HTML file - no dependencies, no build tools, no tracking.

- Open `index.html` directly in a browser, or
- Serve it with any static file host.

## Disclaimer

This tool is for educational purposes only and does not constitute financial advice. Simulated results assume independent, identically distributed trade outcomes and fixed-fractional sizing; real markets and real execution can differ. Past or simulated performance does not guarantee future results.

## License

MIT - see [LICENSE](LICENSE).
