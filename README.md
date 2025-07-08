# stochastic_wealth_simulator
A simulation tool for visualizing the dynamics of multiplicative risk over time. It models wealth evolution for many agents through repeated rounds of binary outcomes (gain or loss), demonstrating how randomness, compounding, and volatility impact long-term outcomes like bankruptcy or exponential growth.

What does it do?
This simulator performs 10,000 Monte Carlo simulations of agents participating in a repeated game. In each round, every player:

Gains +10% with 50% probability
Loses -10% with 50% probability
It tracks wealth evolution across rounds and visualizes key metrics:
Mean & Median wealth over time
25th & 75th percentiles
Fraction of bankrupt players over time
Distribution (histogram) of final wealth
Key statistics like geometric mean & Sharpe-like ratio

Why it matters

This tool helps you understand:
How randomness and compounding interact
Why average outcomes can be misleading in multiplicative games
Why most players can lose even if the mean wealth increases
How volatility leads to inequality and ruin over time

It’s useful for:

Financial modeling
Risk management
Teaching concepts of probability and multiplicative dynamics
Demonstrating wealth distribution in economic simulations

How to Run
Make sure you have Python installed with the required libraries:

pip install numpy matplotlib

You’ll be prompted to enter:

Initial capital: (e.g., 100)

Number of rounds: (e.g., 50–500 recommended)

The simulation will:

Plot wealth trajectories (mean, median, percentiles)
Show how many players go bankrupt over time
Display a histogram of final wealth
Print out key summary metrics

Example Outputs
Mean Wealth vs Median: See divergence due to asymmetry
Fraction < 1: Tracks bankrupt players
Sharpe-like Ratio: Stability of log-returns
% of players achieving 10× returns without bankruptcy
