/*
Title: Path generators and stop conditions
Description: This description will go in the meta description tag
*/

# Path generators and stop conditions

## Path generators

A generator is an algorithm that decides how to traverse a model. Different generators will generate different test sequences, and they will navigate in different ways.

### random

Navigate through the model in a completely random manor. Also called "Drunkard’s walk", or "Random walk". This algorithm selects an out-edge from a vertex by random, and repeats the process in the next vertex.

### quick_random

Tries to run the shortest path through a model, but in a fast fashion. This is how the algorithm works:

Choose an edge not yet visited by random.
Select the shortest path to that edge using Dijkstra's algorithm
Walk that path, and mark all those edges being executed as visited.
When reaching the selected edge in step 1, start all over, repeating steps 1->4.
The algorithm works well an very large models, and generates reasonably short sequences. The downside is when useed in conjunction with ESFM. The algorithm can choose a path which is blocked by a guard.

### a_star

Will generate the shortest path to a specific vertex.

### shortest_all_paths

Will calculate and generate the shortest path through the model. This algorithm is not recommended to use, because for larger models, and using data in the model (EFSM), it will take a considerable time to calculate.

## Stop conditions

### edge_coverage

The stop criteria is a percentage number. When, during execution, the percentage of traversed edges is reached, the test is stopped. If an edge is traversed more than one time, it still counts as 1, when calculating the percentage coverage.

### vertex_coverage

The stop criteria is a percentage number. When, during execution, the percentage of traversed states is reached, the test is stopped. If vertex is traversed more than one time, it still counts as 1, when calculating the percentage coverage.

### reached_vertex

The stop criteria is a named vertex. When, during execution, the vertex is reached, the test is stopped.

### reached_edge

The stop criteria is a named edge. When, during execution, the edge is reached, the test is stopped.

### time_duration

The stop criteria is a time, representing the number of seconds that the test generator is allowed to execute.

### never

This special stop condition will never halt the generator.

