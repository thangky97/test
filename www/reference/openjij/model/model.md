---
sidebar_label: model
title: openjij.model.model
---

| This module defines the BinaryQuadraticModel with the Hamiltonian,

.. math::

    H = \\sum_{i\\neq j} J_{ij}\\sigma_i \\sigma_j + \\sum_{i} h_{i}\\sigma_i,

| in an Ising form and

.. math::

    H = \\sum_{ij} Q_{ij}x_i x_j + \\sum_{i} H_{i}x_i,

| in a QUBO form.
| The methods and usage are basically the same as `dimod <https://github.com/dwavesystems/dimod>`_.

## cimod

## cxxcimod

## dimod

## cxxjij

#### make\_BinaryQuadraticModel

```python
def make_BinaryQuadraticModel(linear: dict, quadratic: dict, sparse)
```

BinaryQuadraticModel factory.

**Returns**:

  generated BinaryQuadraticModel class

#### make\_BinaryQuadraticModel\_from\_JSON

```python
def make_BinaryQuadraticModel_from_JSON(obj: dict)
```

make BinaryQuadraticModel from JSON.

**Returns**:

  corresponding BinaryQuadraticModel type

#### BinaryQuadraticModel

```python
def BinaryQuadraticModel(linear, quadratic, *args, **kwargs)
```

generate BinaryQuadraticModel object.

**Attributes**:

- `vartype` _dimod.Vartype_ - variable type SPIN or BINARY
- `linear` _dict_ - represents linear term
- `quadratic` _dict_ - represents quadratic term
- `offset` _float_ - represents constant energy term when convert to SPIN from BINARY
- `num_variables` _int_ - represents number of variables in the model
- `variables` _list_ - represents variables of the binary quadratic model

**Arguments**:

- `linear` _dict_ - linear biases
- `quadratic` _dict_ - quadratic biases
- `offset` _float_ - offset
- `vartype` _openjij.variable_type.Vartype_ - vartype ('SPIN' or 'BINARY')
- `gpu` _bool_ - if true, this can be used for gpu samplers.
  kwargs:

**Returns**:

  generated BinaryQuadraticModel

**Examples**:

  BinaryQuadraticModel can be initialized by specifing h and J::
  
  >>> h = {0: 1, 1: -2}
  >>> J = {(0, 1): -1, (1, 2): -3, (2, 3): 0.5}
  >>> bqm = oj.BinaryQuadraticModel(self.h, self.J)
  
  You can also use strings and tuples of integers (up to 4 elements) as indices::
  
  >>> h = {'a': 1, 'b': -2}
  >>> J = {('a', 'b'): -1, ('b', 'c'): -3, ('c', 'd'): 0.5}
  >>> bqm = oj.BinaryQuadraticModel(self.h, self.J)

#### bqm\_from\_numpy\_matrix

```python
def bqm_from_numpy_matrix(mat,
                          variables: list = None,
                          offset=0.0,
                          vartype="BINARY",
                          **kwargs)
```

#### BinaryQuadraticModel.from\_numpy\_matrix

#### BinaryQuadraticModel.from\_qubo

#### BinaryQuadraticModel.from\_qubo

#### BinaryQuadraticModel.from\_ising

#### BinaryQuadraticModel.from\_serializable

#### make\_BinaryPolynomialModel

```python
def make_BinaryPolynomialModel(polynomial, index_type=None, tuple_size=0)
```

#### make\_BinaryPolynomialModel\_from\_JSON

```python
def make_BinaryPolynomialModel_from_JSON(obj)
```

#### BinaryPolynomialModel

```python
def BinaryPolynomialModel(*args, **kwargs)
```

#### \_BinaryPolynomialModel\_from\_dict

```python
def _BinaryPolynomialModel_from_dict(polynomial: dict, vartype)
```

#### \_BinaryPolynomialModel\_from\_list

```python
def _BinaryPolynomialModel_from_list(keys: list, values: list, vartype)
```

#### make\_BinaryPolynomialModel\_from\_hising

```python
def make_BinaryPolynomialModel_from_hising(*args, **kwargs)
```

#### \_make\_BinaryPolynomialModel\_from\_hising\_from\_dict

```python
def _make_BinaryPolynomialModel_from_hising_from_dict(polynomial: dict)
```

#### \_make\_BinaryPolynomialModel\_from\_hising\_from\_list

```python
def _make_BinaryPolynomialModel_from_hising_from_list(keys: list,
                                                      values: list)
```

#### make\_BinaryPolynomialModel\_from\_hubo

```python
def make_BinaryPolynomialModel_from_hubo(*args, **kwargs)
```

#### \_make\_BinaryPolynomialModel\_from\_hubo\_from\_dict

```python
def _make_BinaryPolynomialModel_from_hubo_from_dict(polynomial: dict)
```

#### \_make\_BinaryPolynomialModel\_from\_hubo\_from\_list

```python
def _make_BinaryPolynomialModel_from_hubo_from_list(keys: list, values: list)
```

#### \_to\_cxxcimod

```python
def _to_cxxcimod(vartype)
```

#### BinaryPolynomialModel.from\_serializable

#### BinaryPolynomialModel.from\_hising

#### BinaryPolynomialModel.from\_hubo

