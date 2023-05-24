---
sidebar_label: graph_utils
title: openjij.utils.graph_utils
---

## np

#### qubo\_to\_ising

```python
def qubo_to_ising(mat: np.ndarray)
```

inplace-convert numpy matrix from qubo to ising.

**Arguments**:

- `mat` _np.ndarray_ - numpy matrix

#### chimera\_to\_ind

```python
def chimera_to_ind(r: int, c: int, z: int, L: int)
```

[summary]

**Arguments**:

- `r` _int_ - row index
- `c` _int_ - column index
- `z` _int_ - in-chimera index (must be from 0 to 7)
- `L` _int_ - height and width of  chimera-units (total number of spins is :math:`L \\times L \\times 8`)
  

**Raises**:

- `ValueError` - [description]
  

**Returns**:

- `int` - corresponding Chimera index

