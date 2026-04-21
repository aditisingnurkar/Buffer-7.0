# LAIR – Logistics Adaptive Intelligent Routing

## Problem Statement

In logistics networks, a delay at a single hub can propagate through connected routes and disrupt multiple shipments. Traditional routing approaches do not adapt effectively once such disruptions occur, leading to inefficiencies and delivery failures.

---

## Overview

LAIR is a logistics network simulation system that models delivery movement across a multi-stage supply chain. It detects critical bottlenecks, isolates them, and reroutes shipments dynamically using load-aware pathfinding.

The system does not eliminate delays; it minimizes their impact by adapting routing decisions under disrupted conditions.

---

## Data Structures and Algorithms Used

* **Graph (Adjacency List)**
  Represents the logistics network where hubs are nodes and routes are directed edges.

* **Breadth-First Search (BFS)**
  Used to propagate delay across the network based on connectivity and travel time.

* **Priority Queue + Dijkstra’s Algorithm**
  Used for computing optimized routes with a load-aware cost function:

  ```
  cost = α × travel time + β × hub load
  ```

* **Union-Find (Disjoint Set)**
  Used to verify connectivity between hubs before attempting rerouting.

* **Custom Bottleneck Scoring**
  Each hub is evaluated using:

  ```
  score = downstream impact × number of dependent shipments
  ```

---

## System Flow

```
Input → Graph Build → Delay Propagation → Bottleneck Detection
      → Hub Isolation → Rerouting → Output
```

---

## Features

* Detects and isolates critical bottlenecks
* Dynamically reroutes affected shipments
* Handles invalid inputs and unreachable paths
* Tracks shipment status: ACTIVE / DELIVERED / FAILED
* Computes cost improvement after rerouting
* Provides both console output and JavaFX visualization

---

## Input Format

The system reads from a structured text file:

```
HUB <id> <type>
ROUTE <from> <to> <time>
SHIPMENT <id> <path...> | CURRENT <hub>
DELAY <hub> <value>
```

### Example

```
HUB W1 WAREHOUSE
ROUTE W1 S1 5
SHIPMENT SH1 W1 S1 R1 D1 P1 | CURRENT W1
DELAY R2 15
```

---

## Output

* Bottleneck hub and score
* Rerouted paths for affected shipments
* Failed shipments (if unreachable)
* Total cost before and after rerouting
* Percentage improvement
* Final load distribution across hubs

---

## How to Run

1. Place `sample_network.txt` in the project root
2. Run:

   ```
   com.logistics.Main
   ```
3. Use the UI “NEXT” button to step through:

   * Phase 1: Initial state
   * Phase 2: Delay and bottleneck detection
   * Phase 3: Rerouting

---

## Technologies Used

* Java
* JavaFX
* Graph Algorithms (BFS, Dijkstra)
* Union-Find

---

## Project Demo Video

```
https://drive.google.com/file/d/1SSAlpuxXQEnAy3Da4dsF0aTm2E07ARRM/view?usp=sharing
```

---

## Key Takeaway

LAIR demonstrates how a logistics system can remain operational under disruption by adapting routes intelligently. It focuses on resilience and optimization rather than eliminating delays.
