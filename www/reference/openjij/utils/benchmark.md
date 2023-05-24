---
sidebar_label: benchmark
title: openjij.utils.benchmark
---

## inspect

## getLogger

## np

#### logger

#### solver\_benchmark

```python
def solver_benchmark(solver,
                     time_list,
                     solutions=[],
                     args={},
                     p_r=0.99,
                     ref_energy=0,
                     measure_with_energy=False,
                     time_name="execution_time")
```

Calculate 'success probability', 'TTS', 'Residual energy','Standard Error' with computation time

**Arguments**:

- `solver` _callable_ - returns openjij.Response, and solver has arguments 'time' and '**args'
  time_list (list):
  solutions (list(list(int)), list(int)): true solution or list of solution (if solutions are degenerated).
- `args` _dict_ - Arguments for solver.
- `p_r` _float_ - Thereshold probability for time to solutions.
- `ref_energy` _float_ - The ground (reference to calculate success probability and the residual energy) energy.
- `measure_with_energy` _bool_ - use a energy as measure for success

**Returns**:

- `dict` - dictionary which has the following keys:
  
  * **time**: list of compuation time
  * **success_prob** list of success probability at each computation time
  * **tts**: list of time to solusion at each computation time
  * **residual_energy**: list of residual energy at each computation time
  * **se_lower_tts**: list of tts's lower standard error at each computation time
  * **se_upper_tts**: list of tts's upper standard error at each computation time
  * **se_success_prob**: list of success probability's standard error at each computation time
  * **se_residual_energy**: list of residual_energy's standard error at each computation time
  * **info** (dict): Parameter information for the benchmark

#### residual\_energy

```python
def residual_energy(response, ref_energy)
```

Calculate redisual energy from measure energy

**Arguments**:

- `response` _openjij.Response_ - response from solver (or sampler).
- `ref_energy` _float_ - the reference energy (usually use the ground energy)

**Returns**:

- `float` - Residual energy which is defined as :math:`\\langle E \\rangle - E_0` (:math:`\\langle...\\rangle` represents average, :math:`E_0` is the reference energy (usually use the ground energy)).

#### se\_residual\_energy

```python
def se_residual_energy(response, ref_energy)
```

Calculate redisual energy's standard error from measure energy

**Arguments**:

- `response` _openjij.Response_ - response from solver (or sampler).
- `ref_energy` _float_ - the reference energy (usually use the ground energy)

**Returns**:

- `float` - redisual energy's standard error from measure energy

#### success\_probability

```python
def success_probability(response,
                        solutions,
                        ref_energy=0,
                        measure_with_energy=False)
```

Calculate success probability from openjij.response

**Arguments**:

- `response` _openjij.Response_ - response from solver (or sampler).
- `solutions` _list[int]_ - true solutions.

**Returns**:

- `float` - Success probability.
  
  * When measure_with_energy is False, success is defined as getting the same state as solutions.
  * When measure_with_energy is True, success is defined as getting a state which energy is below reference energy

#### se\_success\_probability

```python
def se_success_probability(response,
                           solutions,
                           ref_energy=0,
                           measure_with_energy=False)
```

Calculate success probability's standard error from openjij.response

**Arguments**:

- `response` _openjij.Response_ - response from solver (or sampler).
- `solutions` _list[int]_ - true solutions.

**Returns**:

- `float` - Success probability's standard error.
  
  * When measure_with_energy is False, success is defined as getting the same state as solutions.
  * When measure_with_energy is True, success is defined as getting a state which energy is below reference energy

#### time\_to\_solution

```python
def time_to_solution(success_prob, computation_time, p_r)
```

**Arguments**:

- `success_prob` _float_ - success probability.
  computation_time (float):
- `p_r` _float_ - thereshold probability to calculate time to solution.

**Returns**:

- `float` - time to solution :math:`\\tau * \\log(1-pr)/\\log(1-ps)` which pr is thereshold probability, ps is success probability and :math:`tau` is computation time.

#### se\_lower\_tts

```python
def se_lower_tts(tts, success_prob, computation_time, p_r, se_success_prob)
```

**Arguments**:

- `success_prob` _float_ - success probability.
  computation_time (float):
- `p_r` _float_ - thereshold probability to calculate time to solution.

**Returns**:

- `float` - time to solution :math:`\\tau * \\log(1-pr)/\\log(1-ps)` 's standard error which pr is thereshold probability, ps is success probability and :math:`tau` is computation time.

#### se\_upper\_tts

```python
def se_upper_tts(tts, success_prob, computation_time, p_r, se_success_prob)
```

**Arguments**:

- `success_prob` _float_ - success probability.
  computation_time (float):
- `p_r` _float_ - thereshold probability to calculate time to solution.
  Returens:
- `float` - time to solution :math:`\\tau * \\log(1-pr)/\\log(1-ps)` 's standard error which pr is thereshold probability, ps is success probability and :math:`tau` is computation time.

