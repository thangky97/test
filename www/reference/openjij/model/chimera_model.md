---
sidebar_label: chimera_model
title: openjij.model.chimera_model
---

## SPIN

## cj

## make\_BinaryQuadraticModel

#### make\_ChimeraModel

```python
def make_ChimeraModel(linear, quadratic)
```

ChimeraModel factory.

**Returns**:

  generated ChimeraModel class

#### make\_ChimeraModel\_from\_JSON

```python
def make_ChimeraModel_from_JSON(obj)
```

make ChimeraModel from JSON.

**Returns**:

  corresponding ChimeraModel type

#### ChimeraModel

```python
def ChimeraModel(linear: dict = None,
                 quadratic: dict = None,
                 offset: float = 0.0,
                 vartype=SPIN,
                 unit_num_L: int = None,
                 model=None,
                 gpu: bool = False)
```

generate ChimeraModel object.
This model deal with chimera graph.
ChimeraModel provide methods to verify whether a given interaction graph matches a Chimera graph and to convert it to cxxjij.graph.Chimera.

**Arguments**:

- `linear` _dict_ - linear biases
- `quadratic` _dict_ - quadratic biases
- `offset` _float_ - offset
- `vartype` - vartype ('SPIN' or 'BINARY')
- `unit_num_L` _int_ - unit_num_L
- `model` _BinaryQuadraticModel_ - if model is not None, the object is initialized by model.
- `gpu` _bool_ - if true, this can be used for gpu samplers.

**Returns**:

  generated ChimeraModel
  

**Examples**:

  Example shows how to initialize ChimeraModel.::
  
  # This interactions satisfy chimera topology.
  >>> Q={(0, 4): -1, (4, 12): -1}
  >>> chimera_model = ChimeraModel(Q, unit_num_L=2)  # make
  >>> chimera_self.validate_chimera()

#### ChimeraModel.from\_qubo

#### ChimeraModel.from\_ising

#### ChimeraModel.from\_serializable

