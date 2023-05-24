---
sidebar_label: sqa_sampler
title: openjij.sampler.sqa_sampler
---

## dimod

## np

## get\_state\_and\_energy

## BINARY

## openjij

## oj

## cxxjij

## BaseSampler

## deprecated\_alias

## SQASampler Objects

```python
class SQASampler(BaseSampler)
```

Sampler with Simulated Quantum Annealing (SQA).

Inherits from :class:`openjij.sampler.sampler.BaseSampler`.
Hamiltonian

.. math::

H(s) = s H_p + \\Gamma (1-s)\\sum_i \\sigma_i^x

where :math:`H_p` is the problem Hamiltonian we want to solve.

**Arguments**:

- `beta` _float_ - Inverse temperature.
- `gamma` _float_ - Amplitude of quantum fluctuation.
- `trotter` _int_ - Trotter number.
- `num_sweeps` _int_ - number of sweeps
- `schedule` _list_ - schedule list
- `num_reads` _int_ - Number of iterations.
- `schedule_info` _dict_ - Information about a annealing schedule.
  

**Raises**:

- `ValueError` - If the schedule violates as below.
  - not list or numpy.array.
  - schedule range is '0 <= s <= 1'.

#### parameters

```python
@property
def parameters()
```

#### \_\_init\_\_

```python
@deprecated_alias(iteration="num_reads")
def __init__(beta: Optional[float] = None,
             gamma: Optional[float] = None,
             num_sweeps: Optional[int] = None,
             num_reads: Optional[int] = None,
             schedule: Optional[list] = None,
             trotter: Optional[int] = None)
```

#### \_convert\_validation\_schedule

```python
def _convert_validation_schedule(schedule, beta)
```

#### \_get\_result

```python
def _get_result(system, model)
```

#### sample

```python
def sample(bqm: Union["openjij.model.model.BinaryQuadraticModel",
                      dimod.BinaryQuadraticModel],
           beta: Optional[float] = None,
           gamma: Optional[float] = None,
           num_sweeps: Optional[int] = None,
           schedule: Optional[list] = None,
           trotter: Optional[int] = None,
           num_reads: Optional[int] = None,
           initial_state: Optional[Union[list, dict]] = None,
           updater: Optional[str] = None,
           sparse: Optional[bool] = None,
           reinitialize_state: Optional[bool] = None,
           seed: Optional[int] = None) -> "openjij.sampler.response.Response"
```

Sampling from the Ising model

**Arguments**:

  bqm (openjij.BinaryQuadraticModel) binary quadratic model
- `beta` _float, optional_ - inverse tempareture.
- `gamma` _float, optional_ - strangth of transverse field. Defaults to None.
- `num_sweeps` _int, optional_ - number of sweeps. Defaults to None.
- `schedule` _list[list[float, int]], optional_ - List of annealing parameter. Defaults to None.
- `trotter` _int_ - Trotter number.
- `num_reads` _int, optional_ - number of sampling. Defaults to 1.
- `initial_state` _list[int], optional_ - Initial state. Defaults to None.
- `updater` _str, optional_ - update method. Defaults to 'single spin flip'.
- `reinitialize_state` _bool, optional_ - Re-initilization at each sampling. Defaults to True.
- `seed` _int, optional_ - Sampling seed. Defaults to None.
  

**Raises**:

  ValueError:
  

**Returns**:

- `:class:`openjij.sampler.response.Response`` - results
  

**Examples**:

  
  for Ising case::
  
  >>> h = {0: -1, 1: -1, 2: 1, 3: 1}
  >>> J = {(0, 1): -1, (3, 4): -1}
  >>> sampler = openjij.SQASampler()
  >>> res = sampler.sample_ising(h, J)
  
  for QUBO case::
  
  >>> Q = {(0, 0): -1, (1, 1): -1, (2, 2): 1, (3, 3): 1, (4, 4): 1, (0, 1): -1, (3, 4): 1}
  >>> sampler = openjij.SQASampler()
  >>> res = sampler.sample_qubo(Q)

#### \_annealing\_schedule\_setting

```python
def _annealing_schedule_setting(model,
                                beta=None,
                                gamma=None,
                                num_sweeps=None,
                                schedule=None)
```

#### linear\_ising\_schedule

```python
def linear_ising_schedule(model, beta, gamma, num_sweeps)
```

Generate linear ising schedule.

**Arguments**:

- `model` _:class:`openjij.model.model.BinaryQuadraticModel`_ - BinaryQuadraticModel
- `beta` _float_ - inverse temperature
- `gamma` _float_ - transverse field
- `num_sweeps` _int_ - number of steps

**Returns**:

  generated schedule

#### quartic\_ising\_schedule

```python
def quartic_ising_schedule(model, beta, gamma, num_sweeps)
```

Generate quartic ising schedule based on S. Morita and H. Nishimori, Journal of Mathematical Physics 49, 125210 (2008).

**Arguments**:

- `model` _:class:`openjij.model.model.BinaryQuadraticModel`_ - BinaryQuadraticModel
- `beta` _float_ - inverse temperature
- `gamma` _float_ - transverse field
- `num_sweeps` _int_ - number of steps

**Returns**:

  generated schedule

