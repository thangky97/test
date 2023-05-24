---
sidebar_label: gpu_sa_sampler
title: openjij.sampler.chimera_gpu.gpu_sa_sampler
---

## openjij

## oj

## cxxjij

## BaseGPUChimeraSampler

## SASampler

## GPUChimeraSASampler Objects

```python
class GPUChimeraSASampler(SASampler, BaseGPUChimeraSampler)
```

Sampler with Simulated Annealing (SA) on GPU.

Inherits from :class:`openjij.sampler.sampler.BaseSampler`.

**Arguments**:

- `beta_min` _float_ - Minimum inverse temperature.
- `beta_max` _float_ - Maximum inverse temperature.
- `num_sweeps` _int_ - Length of Monte Carlo step.
- `schedule_info` _dict_ - Information about a annealing schedule.
- `num_reads` _int_ - Number of iterations.
- `unit_num_L` _int_ - Length of one side of two-dimensional lattice in which chimera unit cells are arranged.
  

**Raises**:

- `ValueError` - If variables violate as below.
  - trotter number is odd.
  - no input "unit_num_L" to an argument or this constructor.
  - given problem graph is incompatible with chimera graph.
  
- `AttributeError` - If GPU doesn't work.

#### \_\_init\_\_

```python
def __init__(beta_min=None,
             beta_max=None,
             num_sweeps=1000,
             schedule=None,
             num_reads=1,
             unit_num_L=None)
```

#### sample\_ising

```python
def sample_ising(h,
                 J,
                 beta_min=None,
                 beta_max=None,
                 num_sweeps=None,
                 num_reads=1,
                 schedule=None,
                 initial_state=None,
                 updater=None,
                 reinitialize_state=True,
                 seed=None,
                 unit_num_L=None)
```

sample with Ising model.

**Arguments**:

- `h` _dict_ - linear biases
- `J` _dict_ - quadratic biases
- `beta_min` _float_ - minimal value of inverse temperature
- `beta_max` _float_ - maximum value of inverse temperature
- `num_sweeps` _int_ - number of sweeps
- `num_reads` _int_ - number of reads
- `schedule` _list_ - list of inverse temperature
- `initial_state` _dict_ - initial state
- `updater(str)` - updater algorithm
- `reinitialize_state` _bool_ - if true reinitialize state for each run
- `seed` _int_ - seed for Monte Carlo algorithm
- `unit_num_L` _int_ - number of chimera units
  

**Returns**:

- `:class:`openjij.sampler.response.Response`` - results
  
  Examples::
  
  >>> sampler = openjij.sampler.chimera_gpu.gpu_sa_sampler.GPUChimeraSASampler(unit_num_L=2)
  >>> h = {0: -1, 1: -1, 2: 1, 3: 1},
  >>> J = {(0, 4): -1, (2, 5): -1}
  >>> res = sampler.sample_ising(h, J)

