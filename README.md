
import random
import math
import matplotlib.pyplot as plt
import numpy as np

def estimate_pi(num_samples):
    """Estimates Pi using Monte Carlo simulation."""
    inside_circle = 0
    for _ in range(num_samples):
        x, y = random.random(), random.random()
        if x**2 + y**2 <= 1:
            inside_circle += 1
    return (inside_circle / num_samples) * 4

# Main simulation
sample_sizes = [2**i for i in range(1, 20)]  # [2, 4, 8, ..., 524288]
pi_estimates = []
errors = []

for n in sample_sizes:
    pi_est = estimate_pi(n)
    pi_estimates.append(pi_est)
    errors.append(abs(pi_est - math.pi))

# Visualization
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
plt.plot(sample_sizes, pi_estimates, 'b-', label='Estimated π')
plt.axhline(y=math.pi, color='r', linestyle='--', label='Real π')
plt.xscale('log')
plt.xlabel('Number of Samples (log scale)')
plt.ylabel('π Estimate')
plt.title('Monte Carlo Estimation of π')
plt.legend()

plt.subplot(1, 2, 2)
plt.plot(sample_sizes, errors, 'g--')
plt.xscale('log')
plt.yscale('log')
plt.xlabel('Number of Samples (log scale)')
plt.ylabel('Absolute Error')
plt.title('Convergence Rate')

plt.tight_layout()
plt.savefig('pi_simulation.png')  # Save plot for GitHub
