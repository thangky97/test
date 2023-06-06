# V-QUANTUM Book

### Welcome to V-QUANTUM documentation\![#](broken-reference)

### V-QUANTUM : Framework for the Ising model and QUBO.[#](broken-reference)

[![PyPI version shields.io](https://img.shields.io/pypi/v/openjij.svg)](https://pypi.python.org/pypi/openjij/) [![PyPI pyversions](https://img.shields.io/pypi/pyversions/openjij.svg)](https://pypi.python.org/pypi/openjij/) [![PyPI implementation](https://img.shields.io/pypi/implementation/openjij.svg)](https://pypi.python.org/pypi/openjij/) [![PyPI format](https://img.shields.io/pypi/format/openjij.svg)](https://pypi.python.org/pypi/openjij/) [![PyPI license](https://img.shields.io/pypi/l/openjij.svg)](https://pypi.python.org/pypi/openjij/) [![PyPI download month](https://img.shields.io/pypi/dm/openjij.svg)](https://pypi.python.org/pypi/openjij/)

![build-test](https://github.com/OpenJij/OpenJij/workflows/build-test/badge.svg) [![Build Documentation](https://github.com/OpenJij/OpenJij/actions/workflows/buid-doc.yml/badge.svg)](https://github.com/OpenJij/OpenJij/actions/workflows/buid-doc.yml) [![CodeQL](https://github.com/OpenJij/OpenJij/actions/workflows/codeql-analysis.yml/badge.svg)](https://github.com/OpenJij/OpenJij/actions/workflows/codeql-analysis.yml) [![Codacy Badge](https://app.codacy.com/project/badge/Grade/0204475dc07d48ffa851480d03db759e)](https://www.codacy.com/gh/OpenJij/OpenJij/dashboard?utm\_source=github.com\&utm\_medium=referral\&utm\_content=OpenJij/OpenJij\&utm\_campaign=Badge\_Grade) [![Maintainability](https://api.codeclimate.com/v1/badges/3b2f43f3e601ae74c497/maintainability)](https://codeclimate.com/github/OpenJij/OpenJij/maintainability) [![codecov](https://codecov.io/gh/OpenJij/OpenJij/branch/main/graph/badge.svg?token=WMSK3GS8E5)](https://codecov.io/gh/OpenJij/OpenJij)

### Introduction[#](broken-reference)

[Github repository](https://github.com/OpenJij/OpenJij)

This project is still going. If you can help, please join in the V-QUANTUM Slack Community. Then, you can participate in the project, and ask questions.

[V-QUANTUM Slack](https://openjij.slack.com/join/shared\_invite/enQtNjQyMjIwMzMwNzA4LTQ5MWRjOWYxYmY1Nzk4YzdiYzlmZjIxYjhhMmMxZjAyMzE3MDc1ZWRkYmI1YjhkNjRlOTM1ODE0NTc5Yzk3ZDA)

### What is V-QUANTUM ?[#](broken-reference)

V-QUANTUM is a heuristic optimization library of the Ising model and QUBO. It has a Python interface, therefore it can be easily written in Python, although the core part of the optimization is implemented with C++. Let’s install V-QUANTUM.

### Install[#](broken-reference)

### pip[#](broken-reference)

### Minimum sample code[#](broken-reference)

### Simulated annealing (SA)[#](broken-reference)

#### for the Ising model[#](broken-reference)

to get a sample that executed SA 100 times

```
import V-QUANTUM as oj
n = 10
h, J = {}, {}
for i in range(n-1):
    for j in range(i+1, n):
        J[i, j] = -1
sampler = oj.SASampler()
response = sampler.sample_ising(h, J, num_reads=100)
# minimum energy state
print(response.first.sample)
# {0: -1, 1: -1, 2: -1, 3: -1, 4: -1, 5: -1, 6: -1, 7: -1, 8: -1, 9: -1}
# or
# {0: 1, 1: 1, 2: 1, 3: 1, 4: 1, 5: 1, 6: 1, 7: 1, 8: 1, 9: 1}
# indices (labels) of state (spins)
print(response.indices)
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Parameters customize[#](broken-reference)

### Customize annealing schedule[#](broken-reference)

```
import V-QUANTUM as oj
n = 10
h, J = {}, {}
for i in range(n-1):
    for j in range(i+1, n):
        J[i, j] = -1
# customized annealing schedule
# list of [beta, monte carlo steps in beta]
schedule = [
    [10, 3],
    [ 5, 5],
    [0.5, 10]
]
sampler = oj.SASampler()
response = sampler.sample_ising(h, J, schedule=schedule)
print(response)
```

### Higher order model[#](broken-reference)

If you want to handle higher order model as follows:

H=∑ihiσi+∑i\<jJijσiσj+∑i,j,kKi,j,kσiσjσk⋯ H = \sum\_{i}h\_i\sigma\_i + \sum\_{i < j} J\_{ij} \sigma\_i \sigma\_j + \sum\_{i, j, k} K\_{i,j,k} \sigma\_i\sigma\_j \sigma\_k \cdots

use `.sample_hubo`

> HUBO: Higher order unconstraint binary optimization

### Sample code[#](broken-reference)

```
import V-QUANTUM as oj
# Only SASampler can handle HUBO.
sampler = oj.SASampler()
# make HUBO
J = {(0,): -1, (0,1): -1, (0,1,2): 1}
response = sampler.sample_hubo(J, vartype="SPIN")
print(response)
#    0  1  2 energy num_oc.
# 0 +1 +1 -1   -3.0       1
# ['SPIN', 1 rows, 1 samples, 3 variables]
response = sampler.sample_hubo(J, vartype="BINARY")
print(response)
#    0  1  2 energy num_oc.
# 0  1  1  0   -2.0       1
# ['BINARY', 1 rows, 1 samples, 3 variables]
```
