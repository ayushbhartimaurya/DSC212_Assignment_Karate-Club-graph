# DSC212_Assignment_Karate-Club-graph
Solution to an Assignment of my DSC-212 course, 2nd year BSMS at IISER TVM
# Spectral Modularity for the Karate Club

## Project Overview

This is my notebook for the DSC212 (Graph Theory) research assignment. It's an analysis of the Zachary's Karate Club graph. The main goal was to implement a recursive spectral partitioning algorithm from scratch to find community structures based on modularity.



## Assignment Goals

The assignment required me to:

* **Implement Recursive Spectral Modularity:**
    * Build the modularity matrix: $B = A - \frac{kk^T}{2m}$.
    * Use the leading eigenvector from an eigenvalue decomposition to perform a spectral bisection.
    * Apply this bisection recursively to find communities.
    * Use the $\lambda_1 \le 0$ eigenvalue stopping criterion.
* **Visualize Community Evolution:**
    * Plot the graph after each split, coloring the new communities.
    * Use a fixed node layout so the structure is easy to follow.
* **Compute Network Centrality Metrics:**
    * Calculate Degree, Betweenness, Closeness, and Clustering Coefficient for all nodes after each split.
* **Written Analysis:**
    * Analyze how the metrics change as the communities are split.
    * Compare the final results to the known "ground truth" split of the club.

---

## Implementation Details

### Core Algorithm

* **Modularity Matrix:** I wrote the `calculate_modularity_matrix` function [cell 9] to build the $B$ matrix, making sure it correctly handled subgraphs during recursion.
* **Spectral Bisection:** The bisection logic [cell 11] uses `numpy.linalg.eigh` to find the leading eigenvector of the modularity matrix.
* **Recursive Detection:** The main `recursive_spectral_modularity` function [cell 14] handles the recursion. It keeps splitting a community as long as the modularity gain ($\Delta Q$) is positive.
* **Partition Tracking:** I used a list called `iterations` [cell 14] to store the state of the graph's communities after each successful split.

### Visualization Components

* **Community Evolution Plot:** The `plot_community_evolution` function [cell 17] loops through the `iterations` list and generates a grid of plots showing the graph at each step.
* **Fixed Spring Layout:** To keep the node positions consistent, I used `nx.spring_layout` with a fixed `seed=42` [cell 17].
* **Color-Coded Communities:** I used `matplotlib.cm` [cell 17] to give each new community a distinct color.

### Metric Computation

* **Centrality Metrics:** The `compute_metrics` function [cell 19] calculates all four required metrics using NetworkX's built-in functions.
* **Time Series Tracking:** The metrics for each step are stored in the `metrics_evolution` list [cell 19].

### Analysis & Reporting

* **Metric Evolution Plots:** The `plot_metrics_evolution` function [cell 22] creates plots for each of the four metrics to show how they change over time.
* **Written Discussion:** The notebook also includes markdown cells where I analyze the central nodes [cell 25] and discuss how the metrics are influenced by the community structure [cell 29].

---

## Technical Stack

* **Python 3.x**
* **NetworkX:** For the graph object, loading the data, and running centrality calculations [cell 3, 5, 19].
* **NumPy:** For all the matrix math and the eigenvalue decomposition (`numpy.linalg.eigh`) [cell 3, 11].
* **Matplotlib:** For all the plotting [cell 3, 17, 22].

---

## Mathematical Foundation

* **Modularity Matrix:** $B = A - \frac{kk^T}{2m}$
* **Modularity Gain (from split):** $\Delta Q = \frac{s^T B_{sub} s}{4m_{sub}}$
* **Stopping Criterion:** A split is only accepted if the modularity gain $\Delta Q > 0$ [cell 14] (which is derived from $\lambda_1 > 0$).

---

## Results

* The final algorithm successfully partitioned the 34-node graph. It ran for 10 split iterations, finding 11 final communities [cell 15 output].
* The metric evolution for all 34 nodes was successfully tracked across all 10 iterations [cell 21 output].
* Entire report have been written in the end of .ipynb file.

---

## References

1.  M. E. J. Newman, “Modularity and community structure in networks,” Proceedings of the National Academy of Sciences, 103(23), 8577–8582, 2006. [cell 31]
2.  W. W. Zachary, “An information flow model for conflict and fission in small groups,” Journal of Anthropological Research, 33(4), 452–473, 1977. [cell 31]
3.  NetworkX Developers, “NetworkX documentation: karate\_club\_graph,” https://networkx.org/, accessed 2025. [cell 31]
