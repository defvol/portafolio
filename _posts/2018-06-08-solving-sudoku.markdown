---
layout: post
title:  "Solving Sudoku puzzles using constraint programming"
date:   2018-06-08 19:41:14 -0800
categories: posts
---

I’ve been a big fan of [Sudoku][sudoku] puzzles for years but never asked myself how to programmatically solve them - perhaps I didn’t want to ruin the magic.

![sudoku puzzle](https://upload.wikimedia.org/wikipedia/commons/e/e0/Sudoku_Puzzle_by_L2G-20050714_standardized_layout.svg)

_A typical Sudoku puzzle (CC0 from Wikipedia)_

Now that I’m spending a lot of time looking at discrete optimization problems at my job, I’m starting to see everything through the lens of [CSP][csp].

So one afternoon, as I was scribbling on a magazine puzzle, I realized I could use constraint programming for it. Similar to the classic [queens problem][queens], I would define constraint satisfaction and let a backtracking algorithm find a solution.

In less than an hour I got my own implementation running in Python and [OR-Tools][or].

Later I'd find dozens of blogs describing differents way of achieving this, but none using OR-Tools. So here it is, my own implementation of a Sudoku solver inspired by a magazine puzzle and a cup of coffee.

{% highlight python %}
def solve(clues):
    solver = pywrapcp.Solver('sudokill')

    bloc = defaultdict(list)
    cell = [0] * 9
    cols = defaultdict(list)

    for i in range(9):
        cell[i] = [0] * 9
        for j in range(9):
            # Define lower and upper bounds per cell
            clue = clues[i][j]
            lb, ub = (clue, clue) if clue else (1, 9)
            cell[i][j] = solver.IntVar(lb, ub, 'cell[%i][%i]' % (i, j))
            # Collect vars for rules for blocks and columns
            bloc[(i // 3, j // 3)].append(cell[i][j])
            cols[j].append(cell[i][j])

    # Add constraints
    for n in range(9):
        # All elements in a row must be different and sum 45
        solver.Add(solver.AllDifferent(cell[n]))
        solver.Add(solver.Sum(cell[n]) == 45)
        # All elements in a col must be different and sum 45
        solver.Add(solver.AllDifferent(cols[n]))
        solver.Add(solver.Sum(cols[n]) == 45)

    # All elements in a block should be different and sum 45
    for q in bloc:
        solver.Add(solver.AllDifferent(bloc[q]))
        solver.Add(solver.Sum(bloc[q]) == 45)

    flat_cells = sum(cell, [])
    db = solver.Phase(flat_cells,
                      solver.CHOOSE_FIRST_UNBOUND,
                      solver.ASSIGN_MIN_VALUE)
    solver.NewSearch(db)
return solver, cell
{% endhighlight %}

### Takeaways

CSP provides an elegant framework to solve problems. As programmers we instinctively jump to imperative conditional logic, but constraint programming lets you zoom out and think of the problem in terms of variables, constraints, and objectives. This means that the algorithm is universal, and you should focus on the problem formulation instead.

### Metadata

- **project**: sudokill
- **code**: [https://github.com/defvol/sudokill][sudokill]
- **technologies**: python, or-tools
- **topics**: constraint programming, constraint satisfaction problem, discrete programming

[sudoku]: https://en.wikipedia.org/wiki/Sudoku
[csp]: https://en.wikipedia.org/wiki/Constraint_satisfaction_problem
[queens]: https://developers.google.com/optimization/cp/queens
[or]: https://developers.google.com/optimization/
[sudokill]: https://github.com/defvol/sudokill
