# Challenge 77

### Graph Gossip

In a small town, rumors spread via a directed graph of gossipers, each person (node) tells secrets to others (edges).

Implement a function to find if there’s a “rumor loop” (cycle) and, if not, return the order in which everyone hears the first rumor (topological sort: sources first).

#### Write your solution below

```rust
// Rust Bytes Challenge Issue #98 Graph Gossip️

use std::collections::HashMap;

pub fn topological_sort(graph: &HashMap<String, Vec<String>>) -> Result<Vec<String>, Vec<String>> {
    // TODO: Implement this function
    todo!()
}

#[cfg(test)]
mod tests {
    use super::*;
    // Helper to validate topo order (checks all edges A->B have pos(A) < pos(B))
    fn is_valid_topo_order(order: &[String], graph: &HashMap<String, Vec<String>>) -> bool {
        let pos: HashMap<&String, usize> = order.iter().enumerate().map(|(i, n)| (n, i)).collect();
        for (from, neighbors) in graph {
            if let Some(&p_from) = pos.get(from) {
                for to in neighbors {
                    if let Some(&p_to) = pos.get(to) {
                        if p_from >= p_to {
                            return false;
                        }
                    } else {
                        return false;
                    } // Missing node? Invalid
                }
            }
        }
        true
    }

    #[test]
    fn test_empty_graph() {
        let graph: HashMap<String, Vec<String>> = HashMap::new();
        assert_eq!(topological_sort(&graph), Ok(vec![]));
    }

    #[test]
    fn test_single_node_no_edges() {
        let mut graph = HashMap::new();
        graph.insert("Alice".to_string(), vec![]);
        let result = topological_sort(&graph).unwrap();
        assert_eq!(result, vec!["Alice"]);
    }

    #[test]
    fn test_single_node_self_loop() {
        let mut graph = HashMap::new();
        graph.insert("Bob".to_string(), vec!["Bob".to_string()]);
        let err = topological_sort(&graph).unwrap_err();
        assert_eq!(err, vec!["Bob"]);
    }

    #[test]
    fn test_simple_dag() {
        let mut graph = HashMap::new();
        graph.insert("A".to_string(), vec!["B".to_string(), "C".to_string()]);
        graph.insert("B".to_string(), vec!["D".to_string()]);
        graph.insert("C".to_string(), vec!["D".to_string()]);
        graph.insert("D".to_string(), vec![]);

        let result = topological_sort(&graph).unwrap();
        assert_eq!(result.len(), 4);
        assert!(is_valid_topo_order(&result, &graph));
    }

    #[test]
    fn test_disconnected_components() {
        let mut graph = HashMap::new();
        graph.insert("X".to_string(), vec!["Y".to_string()]);
        graph.insert("Y".to_string(), vec![]);
        graph.insert("P".to_string(), vec!["Q".to_string()]);
        graph.insert("Q".to_string(), vec![]);

        let result = topological_sort(&graph).unwrap();
        assert_eq!(result.len(), 4);
        assert!(is_valid_topo_order(&result, &graph));
    }

    #[test]
    fn test_simple_cycle() {
        let mut graph = HashMap::new();
        graph.insert("E".to_string(), vec!["F".to_string()]);
        graph.insert("F".to_string(), vec!["G".to_string()]);
        graph.insert("G".to_string(), vec!["E".to_string()]);

        let err = topological_sort(&graph).unwrap_err();
        assert_eq!(err.len(), 3);
        assert!(err.contains(&"E".to_string()));
        assert!(err.contains(&"F".to_string()));
        assert!(err.contains(&"G".to_string()));
    }

    #[test]
    fn test_multiple_cycles() {
        let mut graph = HashMap::new();
        graph.insert("C1".to_string(), vec!["C2".to_string()]);
        graph.insert("C2".to_string(), vec!["C1".to_string()]);
        graph.insert("D1".to_string(), vec!["D2".to_string()]);
        graph.insert("D2".to_string(), vec!["D1".to_string()]);

        let err = topological_sort(&graph).unwrap_err();
        assert_eq!(err.len(), 2);
    }

    #[test]
    fn test_cycle_with_dag() {
        // Mixed: DAG part + cycle
        let mut graph = HashMap::new();
        graph.insert("Start".to_string(), vec!["CycleA".to_string()]);
        graph.insert("CycleA".to_string(), vec!["CycleB".to_string()]);
        graph.insert("CycleB".to_string(), vec!["CycleA".to_string()]);
        graph.insert("End".to_string(), vec![]);

        let err = topological_sort(&graph).unwrap_err();
        assert_eq!(err.len(), 2);
        assert!(err.contains(&"CycleA".to_string()));
        assert!(err.contains(&"CycleB".to_string()));
    }

    #[test]
    fn test_complex_dag_multiple_paths() {
        let mut graph = HashMap::new();
        graph.insert("T1".to_string(), vec!["T2".to_string(), "T3".to_string()]);
        graph.insert("T2".to_string(), vec!["T4".to_string()]);
        graph.insert("T3".to_string(), vec!["T4".to_string(), "T5".to_string()]);
        graph.insert("T4".to_string(), vec!["T6".to_string()]);
        graph.insert("T5".to_string(), vec!["T6".to_string()]);
        graph.insert("T6".to_string(), vec![]);

        let result = topological_sort(&graph).unwrap();
        assert_eq!(result.len(), 6);
        assert!(is_valid_topo_order(&result, &graph));
    }

    #[test]
    fn test_no_duplicate_edges() {
        let mut graph = HashMap::new();
        graph.insert(
            "DupA".to_string(),
            vec!["DupB".to_string(), "DupB".to_string()],
        ); // Dup edge
        graph.insert("DupB".to_string(), vec![]);

        let result = topological_sort(&graph).unwrap();
        assert_eq!(result.len(), 2);
        assert!(is_valid_topo_order(&result, &graph));
    }

    #[test]
    fn test_long_chain() {
        let mut graph = HashMap::new();
        let nodes = (0..10).map(|i| format!("N{}", i)).collect::<Vec<_>>();
        for i in 0..9 {
            graph.insert(nodes[i].clone(), vec![nodes[i + 1].clone()]);
        }
        graph.insert(nodes[9].clone(), vec![]);

        let result = topological_sort(&graph).unwrap();
        assert_eq!(result.len(), 10);
        for i in 0..9 {
            let pos_i = result.iter().position(|n| n == &nodes[i]).unwrap();
            let pos_next = result.iter().position(|n| n == &nodes[i + 1]).unwrap();
            assert!(pos_i < pos_next);
        }
    }

    #[test]
    fn test_isolated_nodes_multiple() {
        let mut graph = HashMap::new();
        graph.insert("Iso1".to_string(), vec![]);
        graph.insert("Iso2".to_string(), vec![]);
        graph.insert("Iso3".to_string(), vec![]);

        let result = topological_sort(&graph).unwrap();
        assert_eq!(result.len(), 3);
    }
}
```
