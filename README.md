$ cat /tmp/aco-sjpp-test/README.md

# Hybrid Ant Colony Optimization with Local Search for the Job Shop Scheduling Problem

This project strengthens a baseline **Ant Colony Optimization (ACO)** algorithm
for the **Job Shop Scheduling Problem (JSSP)** with a **Simulated Annealing
(SA)** local-search stage, and studies how this changes the exploration /
exploitation trade-off of the search.

## Contents

- `JSSP_Hybrid_ACO_SimulatedAnnealing.ipynb` — the full Colab notebook: data
  loading, algorithm implementation, experiments and plots.

## What's inside the notebook

- **Data**: the classical **Fisher & Thompson** benchmark instances FT06
  (6×6), FT10 (10×10) and FT20 (20×5). The notebook fetches the instance files
  itself from the [JSPLIB](https://github.com/tamy0612/JSPLIB) benchmark
  repository, with an embedded offline fallback — no manual uploads needed.
- **Baseline ACO**: operation-pair pheromone encoding with an SPT
  (shortest-processing-time) heuristic; ants build a full schedule by
  repeatedly picking the next "ready" operation; the resulting machine
  sequences are evaluated with a disjunctive-graph longest-path pass.
- **Local search**: Simulated Annealing over the classic
  Van Laarhoven–Aarts–Lenstra neighbourhood (adjacent swaps within critical
  blocks on the same machine), applied to the best ant of each iteration
  before the pheromone update — this is what turns the baseline into the
  **hybrid** algorithm.
- **Pheromone strategy study**: sensitivity to the evaporation rate `ρ` and to
  elitist (global-best) vs. iteration-best pheromone reinforcement.
- **SA sensitivity study**: sensitivity to the initial temperature and cooling
  rate.
- **Evaluation**: baseline vs. hybrid compared over multiple random seeds on
  makespan, gap to the known optimum, convergence speed, and how both scale
  from FT06 up to FT10/FT20.

## Running it

Open `JSSP_Hybrid_ACO_SimulatedAnnealing.ipynb` in
[Google Colab](https://colab.research.google.com) (`File → Upload notebook`)
and `Runtime → Run all`. It only needs `numpy`, `pandas` and `matplotlib`,
all of which are preinstalled on Colab.

## Key result

On FT06 the hybrid ACO+SA reaches the known optimal makespan (55), while
baseline ACO alone stalls around 66–69 under the same iteration budget. On the
larger FT10/FT20 instances, the hybrid roughly halves the optimality gap
compared to the baseline (e.g. FT10: ~54% → ~12% gap).
