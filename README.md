#!/usr/bin/env python3
"""
Graphviz DOT generator utility — export directed/undirected graphs to DOT format.
Run: python3 src/graphviz_dot_generator.py
"""
from typing import Dict, List

def to_dot(adj: Dict[str, List[str]], directed=False, name="G"):
    kind = "digraph" if directed else "graph"
    edge_op = "->" if directed else "--"
    lines = [f"{kind} {name} {{"]
    for src, outs in adj.items():
        if not outs:
            lines.append(f'  "{src}";')
        for dest in outs:
            lines.append(f'  "{src}" {edge_op} "{dest}";')
    lines.append("}")
    return "\n".join(lines)

def demo():
    adj = {"A": ["B","C"], "B": ["C"], "C": []}
    print(to_dot(adj, directed=True, name="Demo"))

if __name__ == "__main__":
    demo()
