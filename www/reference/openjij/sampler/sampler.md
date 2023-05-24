---
sidebar_label: sampler
title: openjij.sampler.sampler
---

This module defines the abstract sampler (BaseSampler).

## time

## dimod

## np

## get\_state\_and\_energy

## BINARY

## SPIN

## samplemixinmethod

## openjij

## oj

## cxxjij

#### measure\_time

```python
def measure_time(func)
```

Decorator for measuring calculation time.

**Arguments**:

- `func` - decorator function

## BaseSampler Objects

```python
class BaseSampler(dimod.Sampler)
```

Base sampler class of python wrapper for cxxjij simulator

#### parameters

#### properties

#### \_set\_params

```python
def _set_params(**kwargs)
```

#### \_sampling

```python
def _sampling(**kwargs)
```

#### \_cxxjij\_sampling

```python
def _cxxjij_sampling(model,
                     init_generator,
                     algorithm,
                     system,
                     reinitialize_state=None,
                     seed=None,
                     offset=None)
```

Basic sampling function: for cxxjij sampling

**Arguments**:

- `model` _openjij.BinaryQuadraticModel_ - model has a information of instaunce (h, J, Q)
- `init_generator` _callable_ - return initial state, must have argument structure
- `algorithm` _callable_ - system algorithm of cxxjij
- `system` _:obj:_ - [description]
- `reinitialize_state` _bool, optional_ - [description]. Defaults to None.
- `seed` _int, optional_ - seed for algorithm. Defaults to None.
- `offset` _float_ - an offset which is added to the calculated energy
  

**Returns**:

- `:class:`openjij.sampler.response.Response`` - results

#### \_get\_result

```python
def _get_result(system, model)
```

#### sample

```python
@samplemixinmethod
def sample(bqm, **parameters)
```

Sample from a binary quadratic model.

**Arguments**:

  bqm (openjij.BinaryQuadraticModel):
  Binary Qudratic Model
  **parameters:
  See the implemented sampling for additional keyword definitions.
  

**Returns**:

- `:class:`openjij.sampler.response.Response`` - results

#### sample\_ising

```python
@samplemixinmethod
def sample_ising(h, J, **parameters)
```

Sample from an Ising model using the implemented sample method.

**Arguments**:

- `h` _dict_ - Linear biases
- `J` _dict_ - Quadratic biases
  

**Returns**:

- `:class:`openjij.sampler.response.Response`` - results

#### sample\_qubo

```python
@samplemixinmethod
def sample_qubo(Q, **parameters)
```

Sample from a QUBO model using the implemented sample method.

**Arguments**:

- `Q` _dict or numpy.ndarray_ - Coefficients of a quadratic unconstrained binary optimization
  

**Returns**:

- `:class:`openjij.sampler.response.Response`` - results

