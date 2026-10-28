# Consolidated Replication Prompt

Student: Shashwat Shikhar Dwivedi (Roll No. 2427030605). Course: CSE3121, Artificial Intelligence and Soft Computing. Submitted to: Dr. Neha Chaudhary.

This is a refined, single prompt written after the project was finished. It specifies everything needed to reproduce the deliverables. My original, unedited prompts are in `PROMPT_HISTORY.md`.

---

## Role and goal

You are helping me complete the "Algorithmic Implementation of AI approaches with Viva" component (10 marks) of CSE3121. Implement a **Genetic Algorithm (GA) for the Travelling Salesman Problem (TSP)** on 15 Indian cities, validate it against the exact optimum, and produce three deliverables: a Jupyter notebook, a LaTeX report, and a Beamer presentation. The work must be reproducible, correct, and explainable in a viva.

## Deliverable 1: Jupyter notebook (`GA_TSP_Algorithmic_Implementation.ipynb`)

Write clean, commented, presentable code in this order, with a short markdown explanation before each section:

1. **Problem data.** 15 cities (Delhi, Mumbai, Kolkata, Chennai, Bengaluru, Hyderabad, Ahmedabad, Pune, Jaipur, Lucknow, Bhopal, Patna, Chandigarh, Guwahati, Kochi) given as latitude/longitude. Build a distance matrix using the haversine formula (R = 6371 km).
2. **GA design table** with a reason for each choice:
   - Chromosome: permutation of city indices (every chromosome is a valid tour)
   - Fitness: 1 / tour length
   - Selection: tournament, k = 5
   - Crossover: Order Crossover (OX1), probability 0.9
   - Mutation: segment inversion, probability 0.2
   - Elitism: best 2 copied unchanged
   - Population 150, 300 generations, fixed random seeds
3. **Implementation from scratch** (no GA libraries): `tour_length`, `tournament_select`, `order_crossover`, `inversion_mutation`, `genetic_algorithm`. Include a check that all operators preserve valid permutations.
4. **Run and visualise:** print the best tour and runtime, plot the route on a longitude/latitude map with the start city marked, and plot convergence (best-so-far and population average).
5. **Exact validation:** implement Held-Karp dynamic programming (O(n² 2ⁿ)), report the optimum (expected 7478.9 km), the GA's gap to it, and plot the optimal route. Note that a single run can stall in a local optimum.
6. **Experiments** (save figures to `figures/` and tables as CSV):
   - 6.1 GA versus baselines: random search with the same evaluation budget (150 × 300) averaged over 3 seeds, nearest neighbour, and GA over 10 seeds (mean, best, and how many runs reach the optimum).
   - 6.2 Mutation rate in {0, 0.05, 0.2, 0.5, 0.9}, 8 seeds each, 200 generations, shown as a box plot with the optimum line.
   - 6.3 Population size in {10, 30, 100, 300} at an equal budget of 45,000 evaluations, 8 seeds each, shown as a box plot.
7. **Worked Order Crossover example** with 8 cities and fixed cut points (P1 = 1..8, P2 = [3,7,5,1,6,8,2,4], slice at positions 2 to 4) so it can be traced by hand, plus one inversion-mutation example.
8. **Complexity and limitations:** GA is O(G·P·n) time and O(P·n) space, Held-Karp is O(n² 2ⁿ) time and O(n 2ⁿ) space. No optimality guarantee, seed and parameter dependence, premature convergence.
9. **Conclusion** that states only what the experiments actually show.

Do not include a viva-questions section. Do not hard-code the results text: print them from the computed values.

## Deliverable 2: LaTeX report (`report.tex` to `report.pdf`)

A4 article, 11 pt. Title page with the college logo (`college_logo.jpg`), department, course name and code, project title, my name and roll number, "Submitted to: Dr. Neha Chaudhary", academic year 2026-27. Then abstract, table of contents, and sections: Introduction (problem statement with the objective formula, why a GA, objectives), Methodology (data, GA design table, encoding, fitness, selection, crossover, mutation, elitism, pseudocode), Implementation (key code excerpts), Results (all figures and tables from the notebook, each with a short interpretation), Complexity and Limitations, Conclusion. Use the figures saved by the notebook. Compile with `tectonic report.tex` and fix any errors.

## Deliverable 3: Beamer presentation (`beamer/presentation.tex` to `presentation.pdf`)

Madrid theme with the beaver colour theme, about 15 to 17 slides, figures loaded from `../figures/`. Title slide with my full name (also in the footer), roll number, department, course and supervisor. Slides: outline, TSP problem, why a GA and objectives, GA design table, Order Crossover worked example, exact optimum vs GA route, convergence, baselines table, mutation-rate experiment, population-size experiment, complexity and limitations, conclusion. Use `\AtBeginSection` to repeat the outline. Every number on a slide must come from the notebook results. Compile with `tectonic presentation.tex`.

## Quality requirements

- Reproducible: fixed seeds, and running all notebook cells regenerates every figure and CSV.
- Honest: report that the GA is near-optimal on average and finds the optimum in about half the runs, rather than overstating it. Mention the single-run local optimum.
- Verify by running and compiling everything. Report any warnings or failures instead of hiding them.
- Keep the same style as the existing files, and avoid unnecessary extra files.

## Expected headline results (for checking a replication)

| Method | Length (km) | Gap to optimum |
|---|---|---|
| Exact optimum (Held-Karp) | 7478.9 | 0% |
| GA, best of 10 runs | 7478.9 | 0% |
| GA, mean of 10 runs | 7526.9 | 0.6% |
| Nearest neighbour | 9169.4 | 22.6% |
| Random search, same budget | 9930.4 | 32.8% |

The GA reaches the optimum in 5 of 10 runs.
