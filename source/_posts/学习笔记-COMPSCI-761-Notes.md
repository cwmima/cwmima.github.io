---
title: 'COMPSCI 761 Notes'
date: 2020-06-30 09:00:00
intro: "University of Auckland COMPSCI 761 - Artificial Intelligence"
featured_image:
tags: Notes
---

> Course outline sorted out by myself for quick revision
> <i>University of Auckland COMPSCI 761 - Artificial Intelligence</i>

<br/>

## Search
<hr/>

**Problem**
- Problem Space
    - states
    - actions
- Problem
    - initial state
    - goal
- Problem Solving - search for a path in a graph
- Problem Types
    - Single-state problem
        - Deterministic, fully observable  
        - Agent knows exactly which state it will be in; solution is a sequence 
    - Sensorless problem (conformant problem)
        - Non-observable 
        - Agent may have no idea where it is; solution (if any) is a sequence 
    - Contingency problem
        - Nondeterministic and/or partially observable 
        - Percepts provide new information about current state 
        - Solution is a contingent plan or a policy 
        - Often interleaves search & execution 
    - Exploration problem (online problem) 
        - Unknown state space 
<br/>

**Uninformed Search**
- BFS
- DFS
- Iterative Deepening Search
<br/>

Tree Search + Closed List = Graph Search
<br/>

**Informed Search**
- Best-First Search
    - Greedy
    - A*
    - Iterative Deepening A*
    - Weighted A*
- Heuristics
- Bidirectional Heuristic Search
    - Front-to-back (e.g. MM, NBS, GBFHS)
    - Front-to-front
    - Perimeter Search
<br/>

**Local Search**
- Hill Climbing (best child)
- Stochastic Hill Climbing
    - First Choice
    - Random Walking
    - Random Restart
- Local Beam Search (k best children)
    - Stochastic Beam Search
    - Genetic Algorithm
- Simulated Annealing
<br/>

**Adversarial Search**
- Minimax
    - Alpha-beta Pruning
- Expectimax
- Look-ahead Tree
- Monte-Carlo Tree Search
    - Upper Confidence Bound
<br/>

**Planning**
- Languages: State, Goal, State Update
- Predicates: positive/negative, fluent/static, primitive/derived, object level/meta level
<br/>

**Constraint Satisfaction Problem (CSP)**
- Variables, domains, constraints
- Backtracking Search (uninformed) - DFS for CSP
- Heuristics (informed)
- Constraint propagation
    - Forward checking
    - Arc consistency
- Local Search for CSP
<br/>

## Logic
<hr/>

- Entailment
- Inference
- Propositional Logic &nbsp; 命题逻辑
- Horn Clause/Form &nbsp; 霍恩子句
- Modus Ponens &nbsp; 肯定前件
- Resolution &nbsp; 归结
- Forward/Backward Chaining
- First Order Logic
- Unification
- Generalized Modus Ponens
<img src="logic.png" width="450px">

<br/>

## Classic AI
<hr/>

- Expert System (KBS)
- Knowledge Elicitation
- Knowledge Engineering
- Ontology
    - Conceptual Graph
    - Knowledge Interchange Format (KIF)
- Case-Based Reasoning (CBR)
