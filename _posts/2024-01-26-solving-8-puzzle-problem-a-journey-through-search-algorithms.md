---
layout: post
category: mlandai
---

## Introduction

![the 8 puzzle problem]({{site.url}}/images/8puzzle.jpg){:.ioda}
<img src="{{site.url | prepend: site.url}}images/8puzzle.jpg" alt="the 8 puzzle problem" />

The 8-puzzle problem, also known as the N-puzzle, is a classic puzzle that involves arranging numbered tiles in ascending order on a square grid with one empty space. In this post, we'll explore the implementation of three search algorithms – Breadth-First Search (BFS), Depth-First Search (DFS), and A-Star Search (AST) – to solve the 8-puzzle problem. The accompanying simplified Python code provides a practical look at these algorithms.

Complete python implementation of the task can be found in [this](https://github.com/sagrd/8-puzzle-solver) repo.

## The 8-Puzzle Problem

The 8-puzzle consists of a board with movable tiles numbered 1 through 8 and an empty space. The goal is to find a sequence of moves that transforms the initial configuration into the target configuration where tiles are arranged in ascending order. The puzzle can be represented as an N x N grid, and for our case, we focus on the 3x3 grid (m = 3), commonly known as the 8-puzzle.

## Search Algorithms

### 1. Breadth-First Search (BFS)

BFS explores the search space level by level, visiting all nodes at the current level before moving on to the next level. It uses a queue to maintain the frontier of nodes to be explored.

**Simplified Python Code:**

```python
from collections import deque

def bfs(initial_state):
    frontier = deque()
    frontier.append(initial_state)
    explored = set()

    while frontier:
        node = frontier.popleft()
        explored.add(node.state)

        if node.is_goal_state():
            return solution

        for child in node.expand():
            if child.state not in explored:
                frontier.append(child)
                explored.add(child.state)
```

### 2. Depth-First Search (DFS)

DFS explores as far as possible along each branch before backtracking. It uses a stack to keep track of nodes to be explored.

**Simplified Python Code:**

```python
def dfs(initial_state):
    frontier = []
    frontier.append(initial_state)
    explored = set()

    while frontier:
        node = frontier.pop()
        explored.add(node.state)

        if node.is_goal_state():
            return solution

        for child in node.expand():
            if child.state not in explored:
                frontier.append(child)
                explored.add(child.state)
```

### 3. A-Star Search (AST)

A-Star Search is an informed search algorithm that uses a heuristic to guide the exploration.

**Simplified Python Code:**

```python
import heapq

def ast(initial_state):
    frontier = []
    heapq.heapify(frontier)
    heapq.heappush(frontier, (initial_state.heuristic() + initial_state.cost(), initial_state))
    explored = set()

    while frontier:
        _, node = heapq.heappop(frontier)
        explored.add(node.state)

        if node.is_goal_state():
            return solution

        for child in node.expand():
            if child.state not in explored:
                heapq.heappush(frontier, (child.heuristic() + child.cost(), child))
                explored.add(child.state)
```

In the code, `heuristic()` represents the heuristic function, and `cost()` represents the cost function.

**Heuristic Function:**
In the context of the 8-puzzle problem, the heuristic function estimates the distance from the current state to the goal state, guiding the A-Star Search algorithm. The Manhattan Distance heuristic is commonly used for this problem. Here is a simplified Python code snippet for the heuristic function:

```python
function getHeuristic(state):
    md = 0  # Initialize Manhattan Distance to zero
    
    for tile in state.value:
        index = state.value.index(tile)
        correct_row = tile / 3  # Assuming a 3x3 grid
        correct_col = tile % 3
        current_row = index / 3
        current_col = index % 3
        md += abs(correct_row - current_row) + abs(correct_col - current_col)
    
    return md
```

This pseudo code calculates the Manhattan Distance for each tile and accumulates the distances, providing an estimate of the state's proximity to the goal state.

**Cost Function:**

The cost function in the 8-puzzle problem represents the actual cost incurred to reach a particular state from the initial state. In BFS and DFS implementations, the cost is incremented by one for each move. Here is a simplified Python code snippet for the cost function:

```python
function cost_of_path(node):
    cost = 0  # Initialize cost to zero
    
    while node.rootNode is not None:
        cost += 1
        node = node.rootNode
    
    return cost
```

This pseudo code increments the cost for each move in the solution path, providing a measure of the actual steps taken to reach the current state. 

## Conclusion

Solving the 8-puzzle problem provides an excellent opportunity to explore different search algorithms and their implementations. The simplified Python code provided gives a practical look at BFS, DFS, and A-Star Search, showcasing the versatility of these techniques in solving combinatorial search problems. Understanding these algorithms and their trade-offs is fundamental in the field of artificial intelligence and problem-solving.