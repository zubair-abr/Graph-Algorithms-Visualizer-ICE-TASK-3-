# Graph Algorithms Visualizer (Ice Task 3)
## Author - Zubair Abrahams (ST10506538)

A Java Swing desktop application that lets you build a weighted graph by hand — placing vertices, drawing weighted edges between them. A user can then run classic graph algorithms (BFS, DFS, Dijkstra's, Prim) on it, watching each algorithm visit vertices step-by-step instead of only seeing a final answer.

## Project Description

This is a program that allows a user to visually see via a graph how different edge weights between vertices affect the result of different algorithms being applied upon them. This is a mini practical assignment given to students to express their interpretation skills on understanding code, and programming knowledge to show their ability to improve on features or add additional ones to this Graph Visualiser program. Within this project a user will be able to visually see how different algorithms are applied to vertices and edges that connect said vertices. This program allows the user to set the different weights of each edge that connects two vertices and allows the user to place the vertices themselves. 

This started as a base Graph Algorithms Visualizer (vertex/edge drawing, mode-based mouse interaction, and four working algorithms) which I then extended with the enhancements described below.

## Technologies Used

- **Java 25**
- **Java Swing** — all GUI components (`JFrame`, `JPanel`, `JMenuBar`, `JOptionPane`, `Timer`)
- **Maven** — project build and dependency management (`pom.xml`)
- No external libraries — the entire GUI, event handling, and algorithm logic is built on the standard Java library

## How to Run

This project was built and tested in **Apache NetBeans**, but since it's a standard Maven project it will also run any Maven-aware IDE.

### In NetBeans
1. **File → Open Project** → select the project folder.
2. Right-click the project in the Projects panel → **Run**.
   - *Note: use "Run Project", not "Run File" on an individual class — "Run File" bypasses the project's configured main class as this is something i struggled with.*

### Requirements
- JDK 21 or later
- Maven (bundled with most IDEs, or install separately)

## Usage Guide

The application opens with a black canvas and a **Mode** menu that controls what clicking on the canvas does.

### Modes

| Mode | What clicking does |
|---|---|
| **Add a Vertex** | Click an empty spot on the canvas → enter a 1-character vertex ID → a new vertex appears |
| **Add an Edge** | Click two different vertices in a row → enter a weight → a weighted edge is drawn between them |
| **Edit an Edge** | Click an existing edge → enter a new weight → the edge updates immediately |
| **Remove a Vertex** | Click a vertex → it and all its connected edges are removed |
| **Remove an Edge** | Click an edge → it is removed |
| **None** (with an algorithm selected) | Click a vertex to use it as the starting point for the selected algorithm |

### Building a Graph
1. Switch to **Add a Vertex** mode and click around the canvas to place vertices.
2. Switch to **Add an Edge** mode, then click two vertices one after another and enter a weight when prompted.
3. Repeat until your graph is built. Invalid actions (e.g. connecting a vertex to itself, or duplicating an existing edge) are blocked with an explanatory error message rather than failing silently.

### Running an Algorithm
1. Open the **Algorithms** menu and pick **BFS**, **DFS**, **Dijkstra's Algorithm**, or **Prim's Algorithm**. This automatically switches the mode so you can select a starting vertex.
2. Click any vertex on the canvas to use it as the start.
3. Watch the animation: vertices highlight yellow one at a time, roughly every 600ms, in the order the algorithm actually visits them.
4. Once every visited vertex has been highlighted, the result is displayed at the bottom of the window:
   - **BFS / DFS** → the traversal order, e.g. `BFS : A -> B -> C -> D`
   - **Dijkstra's** → shortest distance from the start to every other vertex, e.g. `A=20, C=40, D=60`
   - **Prim's** → the minimum spanning tree as child=parent pairs, e.g. `B=A, C=B, D=A`

## Features Added / Enhanced

The starter project already provided vertex/edge drawing, mode-based mouse handling, and four working algorithms (BFS, DFS, Dijkstra's, Prim's) that each returned a final text result. I extended it with three enhancements:

### 1. Step-by-Step Algorithm Visualization
Previously, running an algorithm showed a fixed 1 second "Please wait..." message and then immediatly showed the final text result with no indication of how the algorithm 'travelled' to get there. I changed every algorithm to record the order it travels to each vertex (with a new `getTravelOrder()` method added to the `GraphAlgorithm.java` interface and implemented in all four algorithms), and replaced the fixed timer in `Graph.java` with a repeating `Timer` that highlights one vertex at a time before showing the final result. This makes the animation or process of the algorithm visible, not just a static output.

### 2. Input Validation and Error Messages
The original code silently rejected invalid input (e.g. a mistyped vertex ID, or an edge weight that wasn't a valid number) by simply reopening the input dialog with no explanation. I added:
- A block on self-loops (connecting a vertex to itself)
- A clear warning when trying to add a duplicate edge between two already-connected vertices
- Specific error dialogs explaining *why* a vertex ID or edge weight was rejected, instead of a silent retry

### 3. Edge Weight Editing
Originally, an edge's weight was fixed once created — the only way to change it was to delete the edge and redraw it. I added a new **Edit an Edge** mode: clicking an existing edge opens a dialog to enter a new weight, which updates the edge's internal weight and its on-screen label immediately. 

## Skills Applied

- **Java Swing GUI development** — `JFrame`, `JPanel`, custom `paintComponent()` rendering, `JMenuBar`/`JMenuItem`, `JOptionPane` dialogs
- **Event-driven programming** — `MouseListener`, `ActionListener`, mode-based state management via an enum
- **Object-oriented design** — interfaces (`GraphAlgorithm`), enums (`Mode`, `Algorithm`), encapsulation, `equals()`/`hashCode()`/`compareTo()` overrides
- **Data structures** — `Map`, `List`, `Set`, `Queue`, `TreeMap`, adjacency-list graph representation
- **Graph algorithms** — Breadth-First Search, Depth-First Search, Dijkstra's shortest path, Prim's minimum spanning tree
- **Timer-based animation** — using `javax.swing.Timer` to drive a step-by-step visual sequence
- **Defensive programming** — input validation and user-facing error handling

## Visuals

![Graph before any vertices and edges](<img width="781" height="591" alt="image" src="https://github.com/user-attachments/assets/e4a62010-7e81-4f7b-bc5c-b749c8e15fc2" />
)
![Graph before running an algorithm](screenshots/graph-built.png)
![Algorithm mid-animation](screenshots/algorithm-animating.png)
![Final BFS result](screenshots/bfs-result.png)
![Editing an edge weight](screenshots/edit-edge.png)
![Validation error message](screenshots/error-message.png)

## Why This Is a Strong Portfolio Piece

<!-- This section is your own reflection — write it in your own words. Some prompts to get you started: -->

- What did building this teach you about GUI event handling that's different from, say, a console program?
- What was the trickiest bug you ran into, and how did you find/fix it? (e.g. tracing through the Dijkstra's/BFS logic to confirm the visit order was correct)
- Why does this project demonstrate skills relevant to the kind of work you want to do?
- What would you build next if you kept working on it (e.g. save/load, drag-and-drop repositioning, a new algorithm)?
