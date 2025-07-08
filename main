import numpy as np
import matplotlib.pyplot as plt
from datetime import datetime

# Input parameters
initial_capital = float(input("Enter initial capital: "))
n_rounds = int(input("Enter number of rounds: "))

# Set seed for reproducibility
np.random.seed(42)

# Simulation
n_trajectories = 10000
wealth = np.zeros((n_trajectories, n_rounds + 1))
wealth[:, 0] = initial_capital

# Multipliers (1.1 and 0.9)
multipliers = np.where(np.random.rand(n_trajectories, n_rounds) > 0.5, 1.1, 0.9)
for t in range(n_rounds):
    wealth[:, t + 1] = wealth[:, t] * multipliers[:, t]

# Logarithmic wealth (natural logarithm with protection)
log_wealth = np.log(wealth + 1e-10)

# Metrics
mean_wealth = np.mean(wealth, axis=0)
percentiles = np.percentile(wealth, [25, 50, 75], axis=0)
geo_mean = np.exp(np.mean(np.log(wealth + 1e-10), axis=0))

# Fraction with 10x growth without bankruptcy
x10_no_ruin = np.mean(np.max(wealth, axis=1) >= 10 * initial_capital) * 100

# Sharpe-like ratio (per trajectory)
log_returns = np.diff(np.log(wealth + 1e-10), axis=1)
mean_returns = np.mean(log_returns, axis=1)
std_returns = np.std(log_returns, axis=1)
sharpe_like = np.mean(mean_returns / (std_returns + 1e-10))  # Protection against division by zero

# Visualization 1: Mean wealth with percentiles
plt.figure(figsize=(12, 6))
plt.semilogy(range(n_rounds + 1), mean_wealth, label='Mean', color='blue')
plt.semilogy(range(n_rounds + 1), percentiles[1], label='Median (50%)', color='orange')
plt.semilogy(range(n_rounds + 1), percentiles[0], label='25th Percentile', color='green')
plt.semilogy(range(n_rounds + 1), percentiles[2], label='75th Percentile', color='red')
plt.title('Mean Wealth with Percentiles (Logarithmic Scale)')
plt.xlabel('Round')
plt.ylabel('Wealth')
plt.legend()
plt.grid(True, which="both", ls="--")
plt.show()

# Visualization 2: Fraction of bankrupt players over time
ruined_over_time = np.mean(wealth < 1, axis=0)
plt.figure(figsize=(12, 6))
plt.plot(range(n_rounds + 1), ruined_over_time, color='red')
plt.title('Fraction of Bankrupt Players Over Time')
plt.xlabel('Round')
plt.ylabel('Fraction < 1')
plt.grid(True)
plt.show()

# Visualization 3: Histogram of final wealth
plt.figure(figsize=(12, 6))
plt.hist(wealth[:, -1], bins=50, range=(0, 2 * initial_capital), log=True)
plt.title('Histogram of Final Wealth (Logarithmic Scale)')
plt.xlabel('Wealth')
plt.ylabel('Number of Players (Log)')
plt.grid(True, which="both", ls="--")
plt.show()

# Summary
final_wealth = wealth[:, -1]
profit_count = np.sum(final_wealth > initial_capital)
loss_count = np.sum(final_wealth < initial_capital)
ruin_count = np.sum(final_wealth < 1)

# Get current date and time
current_time = datetime.now().strftime("%I:%M %p EEST, %m/%d/%Y")
print(f"Date and time: {current_time}")
print(f"Initial capital: {initial_capital}, Rounds: {n_rounds}, Players: {n_trajectories}")
print(f"Players with profit (> {initial_capital}): {profit_count} ({profit_count/n_trajectories*100:.2f}%)")
print(f"Players with loss (< {initial_capital}): {loss_count} ({loss_count/n_trajectories*100:.2f}%)")
print(f"Bankrupt (< 1): {ruin_count} ({ruin_count/n_trajectories*100:.2f}%)")
print(f"Fraction of trajectories with 10x growth without bankruptcy: {x10_no_ruin:.2f}%")
print(f"Geometric mean (final): {geo_mean[-1]:.4f}")
print(f"Sharpe-like ratio: {sharpe_like:.4f}")
