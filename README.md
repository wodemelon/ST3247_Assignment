# Adaptive-Network Epidemic Parameter Inference

A simulation-based inference project using Approximate Bayesian Computation (ABC) to estimate epidemic and behavioural parameters in an adaptive-network SIR model.

This project was completed as part of the NUS ST3247 module.

## Project Overview

Traditional SIR models assume that the contact network remains fixed throughout an epidemic. In an adaptive-network model, susceptible individuals can break connections with infected neighbours and form new connections elsewhere, allowing behavioural responses such as social distancing to influence disease transmission.

The objective of this project was to infer three unknown model parameters from simulated observations:

- **β (transmission rate):** probability of infection across a susceptible–infected connection
- **γ (recovery rate):** probability that an infected individual recovers
- **ρ (rewiring rate):** probability that a susceptible individual replaces a connection to an infected neighbour

Because the likelihood of the adaptive-network model is difficult to evaluate directly, Approximate Bayesian Computation was used for parameter estimation.

## Data

The observed data contains 40 simulation replicates covering:

- Infected population fraction over time
- Number of network-rewiring events over time
- Final network degree distributions

Summary statistics were constructed from these observations, including epidemic peak, time to peak, total infection burden, rewiring activity and degree-distribution characteristics.

## Methodology

The analysis compared several simulation-based inference approaches:

1. Explored infection trajectories, rewiring activity and final network structure.
2. Designed summary statistics capturing epidemic and network behaviour.
3. Implemented rejection ABC using three different summary-statistic sets:
   - Infection trajectories only
   - Infection and rewiring information
   - Infection, rewiring and final degree distributions
4. Conducted posterior predictive checks against the observed data.
5. Applied PCA-based regression adjustment to refine accepted ABC samples.
6. Implemented Sequential Monte Carlo ABC (SMC-ABC) using progressively tighter acceptance thresholds.

## Key Findings

- Infection trajectories were informative about transmission and recovery dynamics but did not clearly distinguish between transmission and rewiring effects.
- Rewiring counts substantially improved estimation of the rewiring parameter.
- Final network-degree summaries provided additional information about structural changes in the contact network.
- The results demonstrate why combining epidemic and network-level observations is valuable when estimating parameters in adaptive systems.

The final SMC-ABC posterior mean estimates were:

| Parameter | Posterior mean |
|---|---:|
| Transmission rate, β | 0.222 |
| Recovery rate, γ | 0.108 |
| Rewiring rate, ρ | 0.379 |

## Repository Structure

```text
ST3247_Assignment/
├── assignment.ipynb
├── simulator.py
├── data/
│   ├── infected_timeseries.csv
│   ├── rewiring_timeseries.csv
│   └── final_degree_histograms.csv
└── README.md
```

- `assignment.ipynb` contains the complete exploratory analysis, ABC implementation, posterior comparisons and visualisations.
- `simulator.py` contains the provided adaptive-network SIR simulator.
- `data/` contains the observed simulation outputs used for parameter inference.

## Technologies

- Python
- NumPy
- pandas
- Matplotlib
- Jupyter Notebook
- Approximate Bayesian Computation
- Sequential Monte Carlo
