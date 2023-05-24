---
sidebar_label: king_graph
title: openjij.model.king_graph
---

## SPIN

## openjij

## oj

## make\_BinaryQuadraticModel

#### make\_KingGraph

```python
def make_KingGraph(linear=None, quadratic=None, king_graph=None)
```

KingGraph factory

**Returns**:

  generated KingGraph class

#### make\_KingGraph\_from\_JSON

```python
def make_KingGraph_from_JSON(obj)
```

KingGraph factory for JSON

**Arguments**:

- `obj` _dict_ - JSON object

**Returns**:

  generated KingGraph class

#### KingGraph

```python
def KingGraph(linear=None,
              quadratic=None,
              offset=0.0,
              king_graph=None,
              vartype=SPIN,
              machine_type="")
```

generate KingGraph model.

**Arguments**:

- `linear` _dict_ - linear biases
- `quadratic` _dict_ - quadratic biases
- `offset` _float_ - offset
- `king_graph` - represents ising or QUBO interaction.
  Each spins are decided by 2-d corrdinate x, y.
  
  * Quadratic term: [x1, y1, x2, y2, value]
  * Linear term:    [x1, y1, x1, y1, value]
- `vartype` - 'SPIN' or 'BINARY'
- `machine_type` _str_ - choose 'ASIC' or 'FPGA'

**Returns**:

  generated KingGraphModel

**Examples**:

  The following code shows intialization of KingGraph::
  
  >>> h = {}
  >>> J = {(0, 1): -1.0, (1, 2): -3.0}
  >>> king_graph = oj.KingGraph(machine_type="ASIC", linear=h, quadratic=J)
  
  You can initialize it from `king_interaction`::
  
  >>> king_interaction = [[0, 0, 1, 0, -1.0], [1, 0, 2, 0, -3.0]]
  >>> king_graph = oj.KingGraph(machine_type="ASIC", king_graph=king_interaction)

#### KingGraph.from\_qubo

#### KingGraph.from\_ising

#### KingGraph.from\_serializable

