---
sidebar_label: sa_sampler
title: openjij.sampler.sa_sampler
---

## cimod

## dimod

## np

## BINARY

## SPIN

## openjij

## oj

## cxxjij

## BaseSampler

## qubo\_to\_ising

## SASampler Objects

```python
class SASampler(BaseSampler)
```

Sampler with Simulated Annealing (SA).

**Arguments**:

  beta_min (float):
  Minmum beta (inverse temperature).
  You can overwrite in methods .sample_*.
  
  beta_max (float):
  Maximum beta (inverse temperature).
  You can overwrite in methods .sample_*.
  
  num_reads (int):
  number of sampling (algorithm) runs. defaults None.
  You can overwrite in methods .sample_*.
  
  num_sweeps (int):
  number of MonteCarlo steps during SA. defaults None.
  You can overwrite in methods .sample_*.
  
  schedule_info (dict):
  Information about an annealing schedule.
  

**Raises**:

- `ValueError` - If schedules or variables violate as below.
  - not list or numpy.array.
  - not list of tuple (beta : float, step_length : int).
  - beta is less than zero.

#### parameters

```python
@property
def parameters()
```

#### \_\_init\_\_

```python
def __init__(beta_min: Optional[float] = None,
             beta_max: Optional[float] = None,
             num_sweeps: Optional[int] = None,
             num_reads: Optional[int] = None,
             schedule: Optional[list] = None)
```

#### \_convert\_validation\_schedule

```python
def _convert_validation_schedule(schedule)
```

Checks if the schedule is valid and returns cxxjij schedule

#### sample

```python
def sample(bqm: Union["openj.model.model.BinaryQuadraticModel",
                      dimod.BinaryQuadraticModel],
           beta_min: Optional[float] = None,
           beta_max: Optional[float] = None,
           num_sweeps: Optional[int] = None,
           num_reads: Optional[int] = None,
           schedule: Optional[list] = None,
           initial_state: Optional[Union[list, dict]] = None,
           updater: Optional[str] = None,
           sparse: Optional[bool] = None,
           reinitialize_state: Optional[bool] = None,
           seed: Optional[int] = None) -> "oj.sampler.response.Response"
```

sample Ising model.

**Arguments**:

  bqm (openjij.model.model.BinaryQuadraticModel) binary quadratic model
- `beta_min` _float_ - minimal value of inverse temperature
- `beta_max` _float_ - maximum value of inverse temperature
- `num_sweeps` _int_ - number of sweeps
- `num_reads` _int_ - number of reads
- `schedule` _list_ - list of inverse temperature
- `initial_state` _dict_ - initial state
- `updater(str)` - updater algorithm
- `reinitialize_state` _bool_ - if true reinitialize state for each run
- `seed` _int_ - seed for Monte Carlo algorithm

**Returns**:

- `:class:`openjij.sampler.response.Response`` - results
  

**Examples**:

  
  for Ising case::
  
  >>> h = {0: -1, 1: -1, 2: 1, 3: 1}
  >>> J = {(0, 1): -1, (3, 4): -1}
  >>> sampler = openj.SASampler()
  >>> res = sampler.sample_ising(h, J)
  
  for QUBO case::
  
  >>> Q = {(0, 0): -1, (1, 1): -1, (2, 2): 1, (3, 3): 1, (4, 4): 1, (0, 1): -1, (3, 4): 1}
  >>> sampler = openj.SASampler()
  >>> res = sampler.sample_qubo(Q)

#### sample\_hubo

```python
def sample_hubo(
        J: Union[dict, "openj.model.model.BinaryPolynomialModel",
                 cimod.BinaryPolynomialModel],
        vartype: Optional[str] = None,
        beta_min: Optional[float] = None,
        beta_max: Optional[float] = None,
        num_sweeps: Optional[int] = None,
        num_reads: Optional[int] = None,
        schedule: Optional[list] = None,
        initial_state: Optional[Union[list, dict]] = None,
        updater: Optional[str] = None,
        reinitialize_state: Optional[bool] = None,
        seed: Optional[int] = None) -> "openjij.sampler.response.Response"
```

sampling from higher order unconstrainted binary optimization.

**Arguments**:

- `J` _dict_ - Interactions.
- `vartype` _str, openjij.VarType_ - "SPIN" or "BINARY".
- `beta_min` _float, optional_ - Minimum beta (initial inverse temperature). Defaults to None.
- `beta_max` _float, optional_ - Maximum beta (final inverse temperature). Defaults to None.
- `schedule` _list, optional_ - schedule list. Defaults to None.
- `num_sweeps` _int, optional_ - number of sweeps. Defaults to None.
- `num_reads` _int, optional_ - number of reads. Defaults to 1.
- `init_state` _list, optional_ - initial state. Defaults to None.
- `reinitialize_state` _bool_ - if true reinitialize state for each run
- `seed` _int, optional_ - seed for Monte Carlo algorithm. Defaults to None.
  

**Returns**:

- `:class:`openjij.sampler.response.Response`` - results
  
  Examples::
  for Ising case::
  >>> sampler = openjij.SASampler()
  >>> J = {(0,): -1, (0, 1): -1, (0, 1, 2): 1}
  >>> response = sampler.sample_hubo(J, "SPIN")
  
  for Binary case::
  >>> sampler = ooenjij.SASampler()
  >>> J = {(0,): -1, (0, 1): -1, (0, 1, 2): 1}
  >>> response = sampler.sample_hubo(J, "BINARY")

#### geometric\_ising\_beta\_schedule

```python
def geometric_ising_beta_schedule(
        model: openjij.model.model.BinaryQuadraticModel,
        beta_max=None,
        beta_min=None,
        num_sweeps=1000)
```

make geometric cooling beta schedule

**Arguments**:

  model (openjij.model.BinaryQuadraticModel)
- `beta_max` _float, optional_ - [description]. Defaults to None.
- `beta_min` _float, optional_ - [description]. Defaults to None.
- `num_sweeps` _int, optional_ - [description]. Defaults to 1000.

**Returns**:

  list of cxxjij.utility.ClassicalSchedule, list of beta range [max, min]

#### geometric\_hubo\_beta\_schedule

```python
def geometric_hubo_beta_schedule(sa_system, beta_max, beta_min, num_sweeps)
```

