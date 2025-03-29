
# Q8.1: Ablation study on rank $q$ of the SVD approximation

We conducted an ablation study on the SVD rank $q$ across three datasets of varying sizes. The results indicate that increasing q beyond a certain point does not yield continuous performance gains and incurs additional computational cost. Our findings suggest that setting $q$=5 or 7 is optimal, as a small rank is sufficient for nodes to capture neighbor relationship strengths.

| $q$ | AM-Photo | Snap-Patent | Arxiv-Year |
| ----- | -------- | ----------- | ---------- |
| 3     | 88.36    | 71.53       | 64.20      |
| 5     | 90.42    | 72.89       | 66.16      |
| 7     | 90.19    | 73.01       | 66.21      |
| 10    | 90.37    | 72.97       | 66.45      |

# Q8.2: Ablation study on the number of additional edges $\gamma$ in the rewiring strategy

As shown in the Fig. 2 of our paper, the proposed similarity-based graph rewiring method generates a line graph $G^\prime$, where nodes are sequentially connected based on similarity, ensuring each node has at most two neighbors. It obvious that $G^\prime$ is strongly connected.  By adding all edges from $G^\prime$ to the original graph $G$, we obtain the final rewired graph. Compared to the original graph $G$, each node in the rewired graph gains at most two new edges if these edges do not overlap with existing connections.

In the line graph $G^\prime$, the number of additional edges $\gamma$ is fixed. However, to address reviewer jNKj's suggestion, we can add skip connection into $G^\prime$ to increase the number of additional edges. For example, we add a skip connection edge every two nodes, $\gamma$ increases to 3, and so on. In the below table, we can find that increasing the number of additional edges does not improve accuracy, likely due to the introduction of additional noise. Thus, using the simplest line graph $G^\prime$ ensures irreducibility and aperiodicity without compromising accuracy.

| $\gamma$ | AM-Photo | Snap-Patent | Arxiv-Year |
| ---------- | -------- | ----------- | ---------- |
| 2          | 90.42    | 72.89       | 66.16      |
| 3          | 89.27    | 70.09       | 65.37      |
| 4          | 84.10    | 65.54       | 62.88      |

# Q9: Comparison Between the Transformer-Based model and our CGNN

Although we reference paper [6] in our submission as a transformer-based digraph learning model, it is specifically designed for graph-level tasks, and its application to node-level tasks is non-trivial. Instead, DAGTransformer (Luo et al., NeurIPS 2023) is well-suited for node classification tasks. Therefore, we provide a comparison between DAGTransformer and our CGNN at this link:
