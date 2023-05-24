---
sidebar_label: csqa_sampler
title: openjij.sampler.csqa_sampler
---

## np

## openjij

## oj

## cxxjij

## SQASampler

## CSQASampler Objects

```python
class CSQASampler(SQASampler)
```

Sampler with continuous-time simulated quantum annealing (CSQA) using Hamiltonian

.. math::

H(s) = s H_p + \\Gamma (1-s)\\sum_i \\sigma_i^x

where :math:`H_p` is the problem Hamiltonian we want to solve.

**Arguments**:

- `beta` _float_ - Inverse temperature.
- `gamma` _float_ - Amplitude of quantum fluctuation.
- `schedule` _list_ - schedule list
- `step_num` _int_ - Number of Monte Carlo step.
- `schedule_info` _dict_ - Information about a annealing schedule.
- `num_reads` _int_ - Number of iterations.
- `num_sweeps` _int_ - number of sweeps
- `schedule_info` _dict_ - Information about a annealing schedule.

#### \_\_init\_\_

```python
def __init__(beta=5.0, gamma=1.0, num_sweeps=1000, schedule=None, num_reads=1)
```

#### \_get\_result

```python
def _get_result(system, model)
```

#### sample\_ising

```python
def sample_ising(h,
                 J,
                 beta=None,
                 gamma=None,
                 num_sweeps=None,
                 schedule=None,
                 num_reads=None,
                 initial_state=None,
                 updater=None,
                 reinitialize_state=True,
                 seed=None)
```

Sampling from the Ising model.

**Arguments**:

- `h` _dict_ - linear biases
- `J` _dict_ - quadratic biases
- `beta` _float, optional_ - inverse temperature
- `gamma` _float, optional_ - strength of transverse field
- `num_sweeps` _int, optional_ - number of sampling.
- `schedule` _list, optional_ - schedule list
- `num_reads` _int, optional_ - number of iterations
- `initial_state` _optional_ - initial state of spins
- `updater` _str, optional_ - updater algorithm
- `reinitialize_state` _bool, optional_ - Re-initilization at each sampling. Defaults to True.
- `seed` _int, optional_ - Sampling seed.
  

**Returns**:

- `:class:`openjij.sampler.response.Response`` - results
  

**Examples**:

  
  for Ising case::
  
  >>> h = {0: -1, 1: -1, 2: 1, 3: 1}
  >>> J = {(0, 1): -1, (3, 4): -1}
  >>> sampler = openjij.CSQASampler()
  >>> res = sampler.sample_ising(h, J)
  
  for QUBO case::
  
  >>> Q = {(0, 0): -1, (1, 1): -1, (2, 2): 1, (3, 3): 1, (4, 4): 1, (0, 1): -1, (3, 4): 1}
  >>> sampler = openjijj.CSQASampler()
  >>> res = sampler.sample_qubo(Q)

