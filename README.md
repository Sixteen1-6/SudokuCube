# Sudoku Cube Solver Using A* Search

An implementation of the A* search algorithm to solve the Sudoku Cube puzzle - a unique 3x3x3 cube where each face must contain the digits 1-9 exactly once.

## Project Overview

This project implements an intelligent solver for the Sudoku Cube puzzle using the A* search algorithm with custom heuristics. The solver efficiently finds optimal solutions by exploring the state space using admissible heuristics that guide the search towards the goal state.

## Features

- **A* Search Implementation**: Optimal pathfinding algorithm with priority queue
- **Custom Heuristics**: Two complementary heuristics:
  - Duplicate-based heuristic: Counts duplicate digits on each face
  - Adjacency-based heuristic: Measures distance between surplus and deficit faces
- **LRU Cache**: Efficient heuristic caching to avoid redundant computations
- **Memory Monitoring**: Built-in resource management to prevent memory overflow
- **Comprehensive Testing**: Automated testing framework for multiple difficulty levels

## Installation

```bash
# Clone the repository
git clone https://github.com/Sixteen1-6/SudokuCube.git
cd SudokuCube

# Create a conda environment (recommended)
conda create -n sudoku_cube python=3.11
conda activate sudoku_cube

# Install dependencies
pip install -r requirements.txt
```

## Usage

### Basic Usage

```python
from SudokuCube import *

# Create a randomized cube state
state = startingConfig()
randomized_state, moves = CWRandomizer(state, k=10)

# Solve using A* search
rm = ResourceMonitor()
solution = aStarMethod(randomized_state, rm)

# Display solution
if solution['Solved']:
    print(f"Solution found in {len(solution['moves'])} moves!")
    print(f"Moves: {solution['moves']}")
    print(f"Nodes expanded: {solution['nodesExpanded']}")
```

### Running Tests

```python
# Run comprehensive tests
# Format: runTests(trials_per_k, min_k, max_k)
runTests(5, 1, 15)  # 5 trials each for k=1 through k=15
```

### Display Cube State

```python
# Display the cube configuration
displayGUI(state)
```

## Project Structure

```
SudokuCube/
├── SudokuCube.py          # Main implementation
├── README.md              # This file
└── requirements.txt       # Python dependencies
```

## Algorithm Performance

The solver has been tested on various difficulty levels:

| k (Random Moves) | Avg Nodes Expanded | Avg Solution Length | Avg Time (s) |
|------------------|-------------------|---------------------|--------------|
| 1-5              | < 100             | 1-5                 | < 0.1        |
| 6-10             | 100-10,000        | 6-10                | 0.1-5        |
| 11-15            | 10,000+           | 11-15               | 5-60+        |

*Note: Performance varies based on initial configuration and heuristic effectiveness*

## Key Functions

- `startingConfig()`: Returns the solved cube state
- `rotateClock(state, face)`: Rotates a face clockwise
- `rotateCounterClock(state, face)`: Rotates a face counter-clockwise
- `heuristic(state)`: Computes admissible heuristic value
- `aStarMethod(state, monitor)`: Runs A* search algorithm
- `CWRandomizer(state, k)`: Generates random configuration with k clockwise moves
- `displayGUI(state)`: Displays cube in text format