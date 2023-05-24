---
sidebar_label: gpu_sqa_sampler
title: openjij.sampler.chimera_gpu.gpu_sqa_sampler
---

## openjij

## oj

## cxxjij

## BaseGPUChimeraSampler

## SQASampler

## GPUChimeraSQASampler Objects

```python
class GPUChimeraSQASampler(SQASampler, BaseGPUChimeraSampler)
```

Sampler with Simulated Quantum Annealing (SQA) on GPU.

Inherits from :class:`openjij.sampler.sqa_sampler.SQASampler`.

**Arguments**:

- `beta` _float_ - Inverse temperature.
- `gamma` _float_ - Amplitude of quantum fluctuation.
- `trotter` _int_ - Trotter number.
- `num_sweeps` _int_ - number of sweeps
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
def __init__(beta=10.0,
             gamma=1.0,
             trotter=4,
             num_sweeps=100,
             schedule=None,
             num_reads=1,
             unit_num_L=None)
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
                 unit_num_L=None,
                 initial_state=None,
                 updater=None,
                 reinitialize_state=True,
                 seed=None)
```

Sampling from the Ising model

**Arguments**:

- `h` _dict_ - Linear term of the target Ising model.
- `J` _dict_ - Quadratic term of the target Ising model.
- `beta` _float, optional_ - inverse tempareture.
- `gamma` _float, optional_ - strangth of transverse field. Defaults to None.
- `num_sweeps` _int, optional_ - number of sweeps. Defaults to None.
- `schedule` _list[list[float, int]], optional_ - List of annealing parameter. Defaults to None.
- `num_reads` _int, optional_ - number of sampling. Defaults to 1.
- `initial_state` _list[int], optional_ - Initial state. Defaults to None.
- `updater` _str, optional_ - update method. Defaults to 'single spin flip'.
- `reinitialize_state` _bool, optional_ - Re-initilization at each sampling. Defaults to True.
- `seed` _int, optional_ - Sampling seed. Defaults to None.
  

**Returns**:

- `:class:`openjij.sampler.response.Response`` - results
  
  Examples::
  
  >>> sampler = openjij.sampler.chimera_gpu.gpu_sqa_sampler.GPUChimeraSQASampler(unit_num_L=2)
  >>> h = {0: -1, 1: -1, 2: 1, 3: 1},
  >>> J = {(0, 4): -1, (2, 5): -1}
  >>> res = sampler.sample_ising(h, J)

