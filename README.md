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
   - *Note: use "Run Project", not "Run File" on an individual class because "Run File" bypasses the project's configured main class as this is something i struggled with.*

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

Graph before any vertices and edges: 

<img width="781" height="591" alt="Screenshot 2026-09-11 215845" src="https://github.com/user-attachments/assets/ddb04f42-b605-42ad-9369-7b06444f0fb7" />

Graph after adding four (4) vertices: 

<img width="780" height="584" alt="image" src="https://github.com/user-attachments/assets/6a4f25e3-a480-4ed1-898a-149347ddc07c" />

Graph after adding edges to vertices: 

<img width="781" height="586" alt="image" src="https://github.com/user-attachments/assets/58c08a64-57a6-4720-a7c1-c99b9c9509a8" />

Graph during application of algorithm, visualising through highlighting: 

<img width="781" height="590" alt="image" src="https://github.com/user-attachments/assets/6190950b-395c-4f08-a428-cbd9e5e447b2" />

<img width="782" height="588" alt="image" src="https://github.com/user-attachments/assets/275fe0c1-76d5-4a7b-ab3d-8e4ddf94ee84" />


Graph after algorithm applied: 

<img width="781" height="587" alt="image" src="https://github.com/user-attachments/assets/369cf1bc-d6b3-46f6-b43a-32761393cfa7" />


Editing an edge: 

<img width="778" height="587" alt="image" src="https://github.com/user-attachments/assets/269b41fa-296c-4d45-a4fd-22f1cae632ad" />

<img width="782" height="245" alt="image" src="https://github.com/user-attachments/assets/a9da42cd-d96f-4642-a910-b5fc358741e4" />


Error messages and prevention: 

<img width="779" height="588" alt="image" src="https://github.com/user-attachments/assets/b436b210-9229-4036-ab3b-f340d009b806" />

<img width="780" height="584" alt="image" src="https://github.com/user-attachments/assets/ef9bc5c4-1ba0-4633-b552-d83357d2b397" />

<img width="777" height="585" alt="image" src="https://github.com/user-attachments/assets/18ac0cf4-c48b-47d2-87c8-292dd866e65b" />


## Why This Is a Strong Portfolio Piece

I believe this is a strong portfolio piece because it was not just tutorial-based programming where I could use a textbook to cover most of the problems. This pushed my thinking and adaptation skills. This shows how I can read code that I was unfamiliar by, understand how it functions enough to where I could extend upon it, and make design changes. An example of this would be where I added the functionality to edit a weight of an edge between two vertices and realized that both directional copies of that edge otherwise the algorithms would give incorrect results. Catching this issue came to me like instinct instead of trial and error which made me realize that I could understand the code and not just copying and pasting lines of code that is hardwired in my head after studying. This assignment allowed for me to utilize critical thinking and think beyond just what's in front of me but how what I code in one class can affect other classes and how that can produce errors and bugs before it's able to be executed. 

The most challenging thing I approached was adding the algorithm visualization feature. The logic behind running the algorithms were already there, however figuring out how to make the GUI present what the algorithm was doing without causing any bugs or errors especially with the algorithms themselves was difficult. I had to read through each algorithm file (java class files) to understand the algorithm itself and see where I could implement a variable that can catch the vertices in the order in which the algorithm does. 


