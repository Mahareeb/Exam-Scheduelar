# Exam Scheduelar using Genetic Algorithm

## Project Overview

This project implements a **Genetic Algorithm (GA)** from scratch (no GA libraries) to generate feasible university exam schedules that satisfy all *hard constraints* and optimize *soft constraints* where possible.

The implementation is provided in a well-documented Jupyter notebook (`exam_scheduler.ipynb`) and a one-page report (`Report.pdf`). Only **NumPy** and **Pandas** are used for data handling and numerical operations.

---

## Key Objectives

* Read exam-related data (courses, students, teachers) from CSV files.
* Encode a complete exam schedule as a chromosome.
* Apply **roulette wheel selection** to choose parents.
* Implement crossover and mutation strategies to evolve schedules.
* Strictly enforce hard constraints and optimize soft constraints.
* Produce an output table listing course, day, time, duration, and invigilator.
* Log fitness values for each generation and evaluate final constraint satisfaction.

---

## Hard Constraints (Enforced)

* Every course must have an exam scheduled.
* A student cannot have two exams at the same time.
* Exams can only be scheduled Monday–Friday (no weekends).
* Exam start times are between 09:00 and 17:00.
* Each exam must be invigilated by a teacher.
* A teacher cannot invigilate two exams at the same time.
* A teacher cannot invigilate two consecutive exam slots.

---

## Soft Constraints (Optimized)

* Friday 13:00–14:00 should be kept free where possible.
* Students should not have back-to-back exams.
* MG courses should preferably be scheduled before CS courses for students taking both.
* Teacher schedules should be balanced to avoid overload.

The notebook reports which soft constraints are satisfied in the final schedule and provides a score breakdown.

---

## Repository Structure

```
/ (project root)
├─ data/
│  ├─ courses.csv           # course_code, duration, teacher
│  ├─ studentCourse.csv     # student_id, enrolled_courses (comma separated)
│  ├─ studentName.csv       # student_id, student_name
│  └─ teachers.csv          # teacher_id, teacher_name
│
├─ exam_scheduler.ipynb     # main notebook: data load, GA, evaluation, visualization
├─ Report.pdf               # one-page summary report
└─ README.md                # this file
```

*Note: The dataset uses simple CSV formats and is parsed directly in the notebook.*

---

## How to Run

1. Install required libraries:

   ```bash
   pip install numpy pandas jupyter
   ```

2. Launch Jupyter Notebook:

   ```bash
   jupyter notebook
   ```

3. Open **exam_scheduler.ipynb** and run all cells. The notebook is structured into:

   * Data Loading
   * Encoding
   * GA Operators
   * Fitness & Constraints
   * Visualization
   * Output

---

## Chromosome Encoding

A chromosome encodes the assignment of each exam to:

* **Day** (Monday–Friday)
* **Time slot** (start hour)
* **Invigilator** (teacher)

The chosen encoding is explained in the notebook with justification.

---

## Genetic Operators

* **Selection:** Roulette wheel selection based on fitness values.
* **Crossover:** One or more crossover strategies are applied to combine parent schedules.
* **Mutation:** A small percentage of genes are randomly changed (day/time/teacher) using a configurable mutation rate.

---

## Fitness Function

The fitness function combines:

* **Hard constraint penalties** — large penalties for any violation, making such solutions infeasible.
* **Soft constraint bonuses** — additional points for satisfying scheduling preferences.

The notebook displays fitness progression across generations with plots and tables.

---

## Constraint Handling Strategy

* **Hard constraints**: enforced through repair functions during crossover/mutation, and/or large penalties in the fitness function.
* **Soft constraints**: guide the search toward more optimal schedules. The final output lists which are satisfied.

---

## Outputs & Visualization

* The final schedule is printed in tabular form in the notebook (course, day, start_time, duration, teacher).
* Fitness progression is logged and visualized.
* A summary of satisfied constraints is displayed at the end.

---

## Notebook Documentation

The notebook includes:

* Explanations for each step and algorithmic choice.
* Parameter tuning experiments (population size, mutation rate, generations).
* A final evaluation cell listing hard and soft constraint satisfaction.

---

## Deliverables for Submission

* `exam_scheduler.ipynb` — Complete implementation
* `Report.pdf` — One-page summary of design, constraints, and results
* `README.md` — Documentation

---

## Configurable Parameters

* `population_size` (default: 100)
* `num_generations` (e.g., 200)
* `crossover_rate` (e.g., 0.8)
* `mutation_rate` (e.g., 0.01–0.05)
* `elitism_count` (top individuals preserved per generation)

All parameters are defined at the top of the notebook for easy adjustment.

---

## Testing & Validation

The notebook includes:

* Validation functions to confirm all hard constraints are met.
* Counting and reporting of soft constraints satisfied.
* Visualization of fitness history and final solution quality.

---

## Notes & Assumptions

* Time slots are discrete (hourly).
* Exam durations are respected for conflict detection.
* Teacher consecutive-slot rules are enforced.
* Room scheduling is **not implemented** in this version.

---
