# Prompt History: GA for TSP (CSE3121 Algorithmic Implementation)

Student: Shashwat Shikhar Dwivedi (Roll No. 2427030605). Submitted to: Dr. Neha Chaudhary.

## How to read this document

- Every quoted prompt is copied verbatim from the saved Claude Code session logs, in order, with my typos left in.
- The notes under each prompt (what was asked, what the AI did, what was decided, what I learned) were written afterwards from those same logs and from the project files. They describe what actually happened.
- Git/GitHub housekeeping prompts (creating the repository, pushing) and questions about how to package the submission are left out, because they are not part of the technical work.
- `REPLICATION_PROMPT.md` is a separate, refined prompt written after the project was finished. It is not part of this history.

## Overview of the work

| Session | Date | Goal | Output |
|---|---|---|---|
| 1 | 26 Oct 2026 | Pick an algorithm, implement it, write the report | Notebook, LaTeX report, figures |
| 2 | 27 Oct 2026 | Presentation and replication material | Beamer slides, this history, replication prompt |

Final project: a Genetic Algorithm for the Travelling Salesman Problem on 15 Indian cities, validated against the exact optimum (Held-Karp), with three experiments (baselines, mutation rate, population size).

## Session 1: Notebook and report (26 Oct 2026)

### Prompt 1
> go through the handout and help me with the 10 makrer component of algorithm implementation and viva i am planning you give me first a jupyter nb file or something while would be hands down implementation type stuff then we compile a presentable latex doc with screenshot and all of the methodology

**What I was asking for.** A two-stage workflow: first a hands-on implementation notebook, then a presentable LaTeX document containing screenshots and the methodology. The target was the 10-mark "Algorithmic Implementation of AI approaches with Viva" component (5 marks implementation, 5 marks viva).

**What the AI did.** It read the handout and found that the task is to pick one approach from heuristic search, adversarial search, neural networks, fuzzy logic or genetic algorithms. It also found an A* grid-pathfinding notebook already in my folder. It did not change anything yet and asked which route I wanted: keep A* and strengthen it (heuristic comparison, nodes-expanded table), or switch to something more distinctive such as a genetic algorithm or fuzzy controller. Its recommendation was to keep A*, because it is the safest to explain in a viva.

**Decision point.** The choice of algorithm was mine, and the AI's own recommendation was the conservative one. This is the most important turn in the project, because it fixed the topic.

### Prompt 2
> i dont think so a* would be noble

**What I meant.** "Noble" was a typo for "novel". A* on a grid is the standard choice, so other students are likely to submit it, and I wanted something that would stand out.

**Why this changed the project.** I overruled the AI's recommendation. It switched to a Genetic Algorithm on the Travelling Salesman Problem. The reasoning behind that choice, as it was laid out in the session:
- A GA is on the syllabus and is easy to visualise (route maps, convergence curves).
- TSP with 15 cities has about 4.4 x 10^10 possible tours, so brute force is not practical, which makes a heuristic method meaningful.
- 15 cities is still small enough to compute the **exact** optimum with Held-Karp dynamic programming (O(n^2 2^n)). That gives an objective ground truth, so the GA can be graded against the true answer instead of only against other heuristics.

**What the AI then built.** The notebook `GA_TSP_Algorithmic_Implementation.ipynb`, written from scratch with no GA libraries:
- Problem data: 15 Indian cities as latitude/longitude, with a haversine distance matrix (R = 6371 km).
- Representation: a permutation of city indices, so every chromosome is automatically a valid tour. Fitness is 1 / tour length.
- Operators: tournament selection (k = 5), Order Crossover OX1 (probability 0.9), segment inversion mutation (probability 0.2), and elitism (best 2 copied unchanged). Population 150, 300 generations, fixed seeds.
- Validation: Held-Karp gives the true optimum of 7478.9 km.
- Experiments: GA against baselines, a mutation-rate sweep, and a population-size sweep at equal evaluation budget.

**Results the notebook produced (from the saved CSV files):**

| Method | Length (km) | Gap to optimum |
|---|---|---|
| Random search (same budget, mean of 3 seeds) | 9930.4 | 32.8% |
| Nearest neighbour | 9169.4 | 22.6% |
| GA (mean of 10 runs) | 7526.9 | 0.6% |
| GA (best of 10 runs) | 7478.9 | 0.0% |
| Exact optimum (Held-Karp) | 7478.9 | 0.0% |

The GA reached the true optimum in 5 of 10 runs.

**What I learned from the experiments.**
- *Mutation rate.* With no mutation (rate 0) the mean tour was 8079.0 km, clearly the worst. Rates of 0.05 to 0.5 gave means between 7532 and 7661 km, and 0.9 gave 7478.9 km. Without mutation the population loses diversity and crossover alone cannot create new edges, so the search stalls. In this small problem even a very high rate did well, which I would not expect to hold for larger instances.
- *Population size.* At an equal budget of 45,000 evaluations, population 10 had a mean of 7683.1 km and population 300 had 7518.9 km. Larger populations did better here, because diversity matters more than the number of generations at this problem size.
- *Honest reporting of a weak run.* The headline run in the notebook (seed 42) ended at 7745.4 km, about 3.6% above the optimum, because it got stuck in a local optimum. The AI kept that run and added a note instead of picking a lucky seed. It is a concrete example of premature convergence and a good talking point for the viva.

### Prompt 3
> get rid of the viva questions section keep this nb presentable as well and start with the compiling of the latex file use the figures you picked i have added the college logo as well my name is Shashwat Shikhar Dwivedi roll no 2427030605 Submitted to Dr.Neha Chaudhary

**What I was asking for.** Three things: remove the viva Q&A section from the notebook (I wanted to prepare for the viva myself instead of reading ready-made answers), make the notebook presentable, and compile the LaTeX report using the generated figures and my college logo, with my name, roll number and supervisor on the title page.

**What the AI did.**
- Removed the viva section and added my details to the notebook header, then re-ran the whole notebook (23 cells, no errors).
- Built `report.tex` / `report.pdf` (9 pages): introduction and problem statement; methodology with the GA design table, a worked Order Crossover example, pseudocode, Held-Karp and code excerpts; results with five figures and four tables; complexity analysis; limitations; conclusion.
- Pointed out two details it had inferred and I should check: "Department of Computer Science and Engineering" and "Academic Year 2026-27" on the title page. It also warned that an older notebook copy in my Downloads folder still contained the viva section.

**Why the viva removal mattered.** The point of the viva marks is to explain the algorithm myself. For that I rely on the worked crossover example, the complexity section and the limitations section, which are all in the report.

## Session 2: Presentation and replication material (27 Oct 2026)

### Prompt 1
> [Pasted the full Overleaf help article "Beamer" (about 3,000 words: title page, table of contents, overlays, blocks, themes, fonts, columns, and a themes reference table), followed by:] "use this latex beamer template and give me presentable ppt or pdf compiled from it which i can turn in"

**What happened.** I pasted a Beamer tutorial as a template but did not say what the slides should be about. The AI guessed and made a 21-slide deck about Beamer itself, and flagged that it had guessed and asked for the real topic.

**What I learned.** A prompt needs the subject as well as the format. The missing topic cost one round trip.

### Prompt 2
> about the topic itslef like the project we have made ga tsp one

**What I was asking for.** Rebuild the deck around the GA-TSP project instead.

**What the AI did.** It produced a 17-slide Beamer deck (Madrid theme) from the notebook results and figures:
1. Title slide with name, roll number, course and supervisor.
2. The TSP problem and why it is hard (about 4.4 x 10^10 tours).
3. Why a GA, and the project objectives.
4. GA design: encoding, selection, crossover, mutation, elitism.
5. A worked Order Crossover example, for the viva.
6. The exact Held-Karp route (7478.9 km) next to a GA run (7745.4 km).
7. The convergence plot.
8. The baselines table.
9. Mutation-rate and population-size experiments.
10. Complexity and limitations.
11. Conclusion and thank-you.

All numbers on the slides come from the notebook, so slides, report and notebook agree.

### Prompt 3
> [Image #3] change the name to Shashwat Shikhar Dwivedi

**What happened.** The footer on the slides showed a shortened name. I attached a screenshot and asked for the full name. The AI changed it and recompiled, and noted that it had not re-rendered the slide afterwards, so I checked that visually.

### Prompt 4
> i am supposed to submitt prompt history as well to maam she was saying she should be able to replicate the project file so please help me here

**What I was asking for.** A prompt history that lets the course instructor reproduce the project.

**What the AI did.** It extracted my prompts word for word from the two saved session logs, added a one-line note under each, and wrote a replication section. This file is the expanded version of that first draft.

### Prompt 5
> no like what i have done is like very basic stuff in prompting but like she would grade me on the basis of that so give me better promt to submitt to maam

**What I was asking for.** A better prompt, because I felt my own prompts were basic.

**What the AI said.** It offered to write a much stronger prompt but advised me not to present it as what I typed in the moment, since the assignment asks for my history and the logs show the real prompts. It recommended submitting two clearly labelled items: this history (what I actually typed) and a consolidated replication prompt (a refined single prompt written afterwards).

**Outcome.** `REPLICATION_PROMPT.md` / `.pdf`, which specifies the notebook (cities, parameters, operators, seeds, experiments, Held-Karp validation), the report and slides structure, quality requirements, and a table of expected results so a replication can be checked.

## Reflection

**How my prompting evolved.** My early prompts were short and goal-oriented. They stated the outcome I wanted and left the design to the AI. That worked for the first stage but cost a round trip in Session 2, when I gave a format without a topic.

**Where my own judgement mattered.** Two decisions were mine and changed the outcome:
1. Rejecting the recommended A* option for a more distinctive project (Prompt 2).
2. Removing the pre-written viva answers so that I would prepare them myself (Prompt 3).

**What I verified rather than trusted.** The notebook computes the exact optimum with Held-Karp, so the GA's quality is checked against ground truth and not only against its own earlier runs. The slide numbers and report tables come from the same saved CSV files as the notebook. The AI itself flagged items I needed to check (title-page department and year, the stale notebook copy, slides it had not visually inspected).

**What I would do differently.** Specify the topic and the audience in the first prompt, state the evaluation criteria from the handout up front, and ask for the experiments I want to defend in the viva (mutation rate, population size) at the start instead of accepting a default set.

## How to replicate

Folder layout:
```
GA_TSP_Algorithmic_Implementation.ipynb        notebook (run all cells)
figures/                                       PNG and CSV outputs, plus college_logo.jpg
Project Report/report.tex -> report.pdf        LaTeX report
Presentation (beamer)/presentation.tex -> .pdf Beamer slides
Prompts/                                       this file and REPLICATION_PROMPT
```

1. **Environment:** Python 3 with `numpy`, `matplotlib`, `pandas`, and Jupyter. The notebook creates `figures/` itself.
2. **Notebook:** open `GA_TSP_Algorithmic_Implementation.ipynb` and run all cells. It builds the 15-city haversine distance matrix, runs the GA (population 150, 300 generations, tournament k=5, OX1 crossover 0.9, inversion mutation 0.2, elitism 2), computes the exact optimum with Held-Karp (7478.9 km), and runs the baseline, mutation-rate and population-size experiments. Seeds are fixed, so results repeat.
3. **Report:** from `Project Report/` run `tectonic report.tex` (or `pdflatex report.tex` twice).
4. **Slides:** `cd "Presentation (beamer)" && tectonic presentation.tex`. The slides read figures from `../figures/`.
