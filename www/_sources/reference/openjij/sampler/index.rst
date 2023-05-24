:py:mod:`openjij.sampler`
=========================

.. py:module:: openjij.sampler


Subpackages
-----------
.. toctree::
   :titlesonly:
   :maxdepth: 3

   chimera_gpu/index.rst


Submodules
----------
.. toctree::
   :titlesonly:
   :maxdepth: 1

   csqa_sampler/index.rst
   response/index.rst
   sa_sampler/index.rst
   sampler/index.rst
   sqa_sampler/index.rst


Package Contents
----------------

Classes
~~~~~~~

.. autoapisummary::

   openjij.sampler.CSQASampler
   openjij.sampler.Response
   openjij.sampler.SASampler
   openjij.sampler.SQASampler



Functions
~~~~~~~~~

.. autoapisummary::

   openjij.sampler.measure_time



.. py:class:: CSQASampler(beta=5.0, gamma=1.0, num_sweeps=1000, schedule=None, num_reads=1)

   Bases: :py:obj:`openjij.sampler.sqa_sampler.SQASampler`

   .. autoapi-inheritance-diagram:: openjij.sampler.CSQASampler
      :parts: 1

   Sampler with continuous-time simulated quantum annealing (CSQA) using

   Hamiltonian.

   .. math::

       H(s) = s H_p + \Gamma (1-s)\sum_i \sigma_i^x

   where :math:`H_p` is the problem Hamiltonian we want to solve.

   :param beta: Inverse temperature.
   :type beta: :class:`float`
   :param gamma: Amplitude of quantum fluctuation.
   :type gamma: :class:`float`
   :param schedule: schedule list
   :type schedule: :class:`list`
   :param step_num: Number of Monte Carlo step.
   :type step_num: :class:`int`
   :param schedule_info: Information about a annealing schedule.
   :type schedule_info: :class:`dict`
   :param num_reads: Number of iterations.
   :type num_reads: :class:`int`
   :param num_sweeps: number of sweeps
   :type num_sweeps: :class:`int`
   :param schedule_info: Information about a annealing schedule.
   :type schedule_info: :class:`dict`

   .. py:attribute:: properties
      

      

   .. py:method:: parameters()
      :property:

      Parameters as a dict, where keys are keyword parameters accepted by the
      sampler methods and values are lists of the properties relevent to each
      parameter.


   .. py:method:: remove_unknown_kwargs(**kwargs) -> Dict[str, Any]

      Remove with warnings any keyword arguments not accepted by the sampler.

      :param \*\*kwargs: Keyword arguments to be validated.

      Returns: Updated `kwargs` dict.

      .. rubric:: Examples

      >>> import warnings
      >>> sampler = dimod.RandomSampler()
      >>> with warnings.catch_warnings():
      ...     warnings.filterwarnings('ignore')
      ...     try:
      ...         sampler.remove_unknown_kwargs(num_reads=10, non_param=3)
      ...     except dimod.exceptions.SamplerUnknownArgWarning:
      ...        pass
      {'num_reads': 10}


   .. py:method:: sample(bqm: Union[openjij.model.model.BinaryQuadraticModel, dimod.BinaryQuadraticModel], beta: Optional[float] = None, gamma: Optional[float] = None, num_sweeps: Optional[int] = None, schedule: Optional[list] = None, trotter: Optional[int] = None, num_reads: Optional[int] = None, initial_state: Optional[Union[list, dict]] = None, updater: Optional[str] = None, sparse: Optional[bool] = None, reinitialize_state: Optional[bool] = None, seed: Optional[int] = None) -> openjij.sampler.response.Response

      Sampling from the Ising model.

      :param bqm:
      :type bqm: :class:`openjij.BinaryQuadraticModel`
      :param beta: inverse tempareture.
      :type beta: :class:`float, optional`
      :param gamma: strangth of transverse field. Defaults to None.
      :type gamma: :class:`float, optional`
      :param num_sweeps: number of sweeps. Defaults to None.
      :type num_sweeps: :class:`int, optional`
      :param schedule: List of annealing parameter. Defaults to None.
      :type schedule: :class:`list[list[float, int]], optional`
      :param trotter: Trotter number.
      :type trotter: :class:`int`
      :param num_reads: number of sampling. Defaults to 1.
      :type num_reads: :class:`int, optional`
      :param initial_state: Initial state. Defaults to None.
      :type initial_state: :class:`list[int], optional`
      :param updater: update method. Defaults to 'single spin flip'.
      :type updater: :class:`str, optional`
      :param reinitialize_state: Re-initilization at each sampling. Defaults to True.
      :type reinitialize_state: :class:`bool, optional`
      :param seed: Sampling seed. Defaults to None.
      :type seed: :class:`int, optional`

      :raises ValueError:

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`

      .. rubric:: Examples

      for Ising case::

          >>> h = {0: -1, 1: -1, 2: 1, 3: 1}
          >>> J = {(0, 1): -1, (3, 4): -1}
          >>> sampler = openjij.SQASampler()
          >>> res = sampler.sample_ising(h, J)

      for QUBO case::

          >>> Q = {(0, 0): -1, (1, 1): -1, (2, 2): 1, (3, 3): 1, (4, 4): 1, (0, 1): -1, (3, 4): 1}
          >>> sampler = openjij.SQASampler()
          >>> res = sampler.sample_qubo(Q)


   .. py:method:: sample_ising(h, J, beta=None, gamma=None, num_sweeps=None, schedule=None, num_reads=None, initial_state=None, updater=None, reinitialize_state=True, seed=None)

      Sampling from the Ising model.

      :param h: linear biases
      :type h: :class:`dict`
      :param J: quadratic biases
      :type J: :class:`dict`
      :param beta: inverse temperature
      :type beta: :class:`float, optional`
      :param gamma: strength of transverse field
      :type gamma: :class:`float, optional`
      :param num_sweeps: number of sampling.
      :type num_sweeps: :class:`int, optional`
      :param schedule: schedule list
      :type schedule: :class:`list, optional`
      :param num_reads: number of iterations
      :type num_reads: :class:`int, optional`
      :param initial_state: initial state of spins
      :type initial_state: :class:`optional`
      :param updater: updater algorithm
      :type updater: :class:`str, optional`
      :param reinitialize_state: Re-initilization at each sampling. Defaults to True.
      :type reinitialize_state: :class:`bool, optional`
      :param seed: Sampling seed.
      :type seed: :class:`int, optional`

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`

      .. rubric:: Examples

      for Ising case::

          >>> h = {0: -1, 1: -1, 2: 1, 3: 1}
          >>> J = {(0, 1): -1, (3, 4): -1}
          >>> sampler = openjij.CSQASampler()
          >>> res = sampler.sample_ising(h, J)

      for QUBO case::

          >>> Q = {(0, 0): -1, (1, 1): -1, (2, 2): 1, (3, 3): 1, (4, 4): 1, (0, 1): -1, (3, 4): 1}
          >>> sampler = openjijj.CSQASampler()
          >>> res = sampler.sample_qubo(Q)


   .. py:method:: sample_qubo(Q, **parameters)

      Sample from a QUBO model using the implemented sample method.

      :param Q: Coefficients of a quadratic unconstrained binary optimization
      :type Q: :class:`dict or numpy.ndarray`

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`



.. py:class:: Response(record, variables, info, vartype)

   Bases: :py:obj:`dimod.SampleSet`

   .. autoapi-inheritance-diagram:: openjij.sampler.Response
      :parts: 1

   Samples and any other data returned by dimod samplers.

   :param record: A NumPy record array. Must have 'sample', 'energy' and 'num_occurrences' as fields.
                  The 'sample' field should be a 2D NumPy array where each row is a sample and each
                  column represents the value of a variable.
   :type record: :class:`:obj:`numpy.recarray``
   :param variables: An iterable of variable labels, corresponding to columns in `record.samples`.
   :type variables: :class:`iterable`
   :param info: Information about the :class:`SampleSet` as a whole, formatted as a dict.
   :type info: :class:`dict`
   :param vartype: Variable type for the :class:`SampleSet`. Accepted input values:

                   * :class:`.Vartype.SPIN`, ``'SPIN'``, ``{-1, 1}``
                   * :class:`.Vartype.BINARY`, ``'BINARY'``, ``{0, 1}``
                   * :class:`.ExtendedVartype.DISCRETE`, ``'DISCRETE'``
   :type vartype: :class:`:class:`.Vartype`/str/set`

   .. rubric:: Examples

   This example creates a SampleSet out of a samples_like object (a NumPy array).

   >>> import numpy as np
   ...
   >>> sampleset =  dimod.SampleSet.from_samples(np.ones(5, dtype='int8'),
   ...                                           'BINARY', 0)
   >>> sampleset.variables
   Variables([0, 1, 2, 3, 4])

   .. py:method:: aggregate()

      Create a new SampleSet with repeated samples aggregated.

      :returns: :obj:`.SampleSet`

      .. note::

         :attr:`.SampleSet.record.num_occurrences` are accumulated but no
         other fields are.

      .. rubric:: Examples

      This examples aggregates a sample set with two identical samples
      out of three.

      >>> sampleset = dimod.SampleSet.from_samples([[0, 0, 1], [0, 0, 1],
      ...                                           [1, 1, 1]],
      ...                                           dimod.BINARY,
      ...                                           [0, 0, 1])
      >>> print(sampleset)
         0  1  2 energy num_oc.
      0  0  0  1      0       1
      1  0  0  1      0       1
      2  1  1  1      1       1
      ['BINARY', 3 rows, 3 samples, 3 variables]
      >>> print(sampleset.aggregate())
         0  1  2 energy num_oc.
      0  0  0  1      0       2
      1  1  1  1      1       1
      ['BINARY', 2 rows, 3 samples, 3 variables]


   .. py:method:: append_variables(samples_like, sort_labels=True)

      Deprecated in favor of `dimod.append_variables`.


   .. py:method:: change_vartype(vartype, energy_offset=0.0, inplace=True)

      Return the :class:`SampleSet` with the given vartype.

      :param vartype: Variable type to use for the new :class:`SampleSet`. Accepted input values:

                      * :class:`.Vartype.SPIN`, ``'SPIN'``, ``{-1, 1}``
                      * :class:`.Vartype.BINARY`, ``'BINARY'``, ``{0, 1}``
      :type vartype: :class:`:class:`.Vartype`/str/set`
      :param energy_offset: Constant value applied to the 'energy' field of :attr:`SampleSet.record`.
      :type energy_offset: :class:`number, optional, defaul=0.0`
      :param inplace: If True, the instantiated :class:`SampleSet` is updated; otherwise, a new
                      :class:`SampleSet` is returned.
      :type inplace: :class:`bool, optional, default=True`

      :returns: SampleSet with changed vartype. If `inplace` is True, returns itself.
      :rtype: :obj:`.SampleSet`

      .. rubric:: Notes

      This function is non-blocking unless `inplace==True`, in which case
      the sample set is resolved.

      .. rubric:: Examples

      This example creates a binary copy of a spin-valued :class:`SampleSet`.

      >>> sampleset = dimod.ExactSolver().sample_ising({'a': -0.5, 'b': 1.0}, {('a', 'b'): -1})
      >>> sampleset_binary = sampleset.change_vartype(dimod.BINARY, energy_offset=1.0, inplace=False)
      >>> sampleset_binary.vartype is dimod.BINARY
      True
      >>> sampleset_binary.first.sample
      {'a': 0, 'b': 0}


   .. py:method:: copy()

      Create a shallow copy.


   .. py:method:: data(fields=None, sorted_by='energy', name='Sample', reverse=False, sample_dict_cast=True, index=False)

      Iterate over the data in the :class:`SampleSet`.

      :param fields: If specified, only these fields are included in the yielded tuples.
                     The special field name 'sample' can be used to view the samples.
      :type fields: :class:`list, optional, default=None`
      :param sorted_by: Selects the record field used to sort the samples. If None, the samples are yielded
                        in record order.
      :type sorted_by: :class:`str/None, optional, default='energy'`
      :param name: Name of the yielded namedtuples or None to yield regular tuples.
      :type name: :class:`str/None, optional, default='Sample'`
      :param reverse: If True, yield in reverse order.
      :type reverse: :class:`bool, optional, default=False`
      :param sample_dict_cast: Samples are returned as dicts rather than
                               :class:`.SampleView`, which requires heavy memory
                               usage. Set to False to reduce load on memory.
      :type sample_dict_cast: :class:`bool, optional, default=True`
      :param index: If True, `datum.idx` gives the corresponding index of the
                    :attr:`.SampleSet.record`.
      :type index: :class:`bool, optional, default=False`

      :Yields: :class:`namedtuple/tuple` -- The data in the :class:`SampleSet`, in the order specified by the input
               `fields`.

      .. rubric:: Examples

      >>> sampleset = dimod.ExactSolver().sample_ising({'a': -0.5, 'b': 1.0}, {('a', 'b'): -1})
      >>> for datum in sampleset.data(fields=['sample', 'energy']):   # doctest: +SKIP
      ...     print(datum)
      Sample(sample={'a': -1, 'b': -1}, energy=-1.5)
      Sample(sample={'a': 1, 'b': -1}, energy=-0.5)
      Sample(sample={'a': 1, 'b': 1}, energy=-0.5)
      Sample(sample={'a': -1, 'b': 1}, energy=2.5)
      >>> for energy, in sampleset.data(fields=['energy'], sorted_by='energy'):
      ...     print(energy)
      ...
      -1.5
      -0.5
      -0.5
      2.5
      >>> print(next(sampleset.data(fields=['energy'], name='ExactSolverSample')))
      ExactSolverSample(energy=-1.5)


   .. py:method:: data_vectors()
      :property:

      The per-sample data in a vector.

      :returns: A dict where the keys are the fields in the record and the
                values are the corresponding arrays.
      :rtype: dict

      .. rubric:: Examples

      >>> sampleset = dimod.SampleSet.from_samples([[-1, 1], [1, 1]], dimod.SPIN,
                                                   energy=[-1, 1])
      >>> sampleset.data_vectors['energy']
      array([-1,  1])

      Note that this is equivalent to, and less performant than:

      >>> sampleset = dimod.SampleSet.from_samples([[-1, 1], [1, 1]], dimod.SPIN,
                                                   energy=[-1, 1])
      >>> sampleset.record['energy']
      array([-1,  1])


   .. py:method:: done()

      Return True if a pending computation is done.

      Used when a :class:`SampleSet` is constructed with :meth:`SampleSet.from_future`.

      .. rubric:: Examples

      This example uses a :class:`~concurrent.futures.Future` object directly. Typically
      a :class:`~concurrent.futures.Executor` sets the result of the future
      (see documentation for :mod:`concurrent.futures`).

      >>> from concurrent.futures import Future
      ...
      >>> future = Future()
      >>> sampleset = dimod.SampleSet.from_future(future)
      >>> future.done()
      False
      >>> future.set_result(dimod.ExactSolver().sample_ising({0: -1}, {}))
      >>> future.done()
      True
      >>> sampleset.first.energy
      -1.0


   .. py:method:: energies()
      :property:


   .. py:method:: filter(pred: Callable[[Any], bool]) -> SampleSet

      Return a new sampleset with rows filtered by the given predicate.

      :param pred: A function that accepts a named tuple as returned by
                   :meth:`.data` and returns a :class:`bool`.

      :returns: A new sample set with only the data rows for which ``pred`` returns
                ``True``.

      .. rubric:: Examples

      >>> sampleset = dimod.SampleSet.from_samples(
      ...     [{'a': 1, 'b': 0}, {'a': 0, 'b': 1}],
      ...     vartype=dimod.BINARY,
      ...     energy=[0, 1],
      ...     is_feasible=[True, False]
      ...     )
      >>> feasible_sampleset = sampleset.filter(lambda d: d.is_feasible)
      >>> print(feasible_sampleset)
         a  b energy num_oc. is_fea.
      0  1  0      0       1    True
      ['BINARY', 1 rows, 1 samples, 2 variables]


   .. py:method:: first()
      :property:

      Sample with the lowest-energy.

      :raises ValueError: If empty.

      .. rubric:: Example

      >>> sampleset = dimod.ExactSolver().sample_ising({'a': 1}, {('a', 'b'): 1})
      >>> sampleset.first
      Sample(sample={'a': -1, 'b': 1}, energy=-2.0, num_occurrences=1)


   .. py:method:: from_future(future, result_hook=None)
      :classmethod:

      Construct a :class:`SampleSet` referencing the result of a future computation.

      :param future: Object that contains or will contain the information needed to construct a
                     :class:`SampleSet`. If `future` has a :meth:`~concurrent.futures.Future.done` method,
                     this determines the value returned by :meth:`.SampleSet.done`.
      :type future: :class:`object`
      :param result_hook: A function that is called to resolve the future. Must accept the future and return
                          a :obj:`.SampleSet`. If not provided, set to

                          .. code-block:: python

                              def result_hook(future):
                                  return future.result()
      :type result_hook: :class:`callable, optional`

      :returns: :obj:`.SampleSet`

      .. rubric:: Notes

      The future is resolved on the first read of any of the :class:`SampleSet` properties.

      .. rubric:: Examples

      Run a dimod sampler on a single thread and load the returned future into :class:`SampleSet`.

      >>> from concurrent.futures import ThreadPoolExecutor
      ...
      >>> bqm = dimod.BinaryQuadraticModel.from_ising({}, {('a', 'b'): -1})
      >>> with ThreadPoolExecutor(max_workers=1) as executor:
      ...     future = executor.submit(dimod.ExactSolver().sample, bqm)
      ...     sampleset = dimod.SampleSet.from_future(future)
      >>> sampleset.first.energy    # doctest: +SKIP


   .. py:method:: from_samples(samples_like, vartype, energy, info=None, num_occurrences=None, aggregate_samples=False, sort_labels=True, **vectors)
      :classmethod:

      Build a :class:`SampleSet` from raw samples.

      :param samples_like: A collection of raw samples. 'samples_like' is an extension of NumPy's array_like_.
                           See :func:`.as_samples`.
      :param vartype: Variable type for the :class:`SampleSet`. Accepted input values:

                      * :class:`.Vartype.SPIN`, ``'SPIN'``, ``{-1, 1}``
                      * :class:`.Vartype.BINARY`, ``'BINARY'``, ``{0, 1}``
                      * :class:`.ExtendedVartype.DISCRETE`, ``'DISCRETE'``
      :type vartype: :class:`:class:`.Vartype`/str/set`
      :param energy: Vector of energies.
      :type energy: :class:`array_like`
      :param info: Information about the :class:`SampleSet` as a whole formatted as a dict.
      :type info: :class:`dict, optional`
      :param num_occurrences: Number of occurrences for each sample. If not provided, defaults to a vector of 1s.
      :type num_occurrences: :class:`array_like, optional`
      :param aggregate_samples: If True, all samples in returned :obj:`.SampleSet` are unique,
                                with `num_occurrences` accounting for any duplicate samples in
                                `samples_like`.
      :type aggregate_samples: :class:`bool, optional, default=False`
      :param sort_labels: Return :attr:`.SampleSet.variables` in sorted order. For mixed
                          (unsortable) types, the given order is maintained.
      :type sort_labels: :class:`bool, optional, default=True`
      :param \*\*vectors: Other per-sample data.
      :type \*\*vectors: :class:`array_like`

      :returns: :obj:`.SampleSet`

      .. rubric:: Examples

      This example creates a SampleSet out of a samples_like object (a dict).

      >>> import numpy as np
      ...
      >>> sampleset = dimod.SampleSet.from_samples(
      ...   dimod.as_samples({'a': 0, 'b': 1, 'c': 0}), 'BINARY', 0)
      >>> sampleset.variables
      Variables(['a', 'b', 'c'])

      .. _array_like:  https://numpy.org/doc/stable/user/basics.creation.html


   .. py:method:: from_samples_bqm(samples_like, bqm, **kwargs)
      :classmethod:

      Build a sample set from raw samples and a binary quadratic model.

      The binary quadratic model is used to calculate energies and set the
      :class:`vartype`.

      :param samples_like: A collection of raw samples. 'samples_like' is an extension of NumPy's array_like.
                           See :func:`.as_samples`.
      :param bqm: A binary quadratic model.
      :type bqm: :class:`:obj:`.BinaryQuadraticModel``
      :param info: Information about the :class:`SampleSet` as a whole formatted as a dict.
      :type info: :class:`dict, optional`
      :param num_occurrences: Number of occurrences for each sample. If not provided, defaults to a vector of 1s.
      :type num_occurrences: :class:`array_like, optional`
      :param aggregate_samples: If True, all samples in returned :obj:`.SampleSet` are unique,
                                with `num_occurrences` accounting for any duplicate samples in
                                `samples_like`.
      :type aggregate_samples: :class:`bool, optional, default=False`
      :param sort_labels: Return :attr:`.SampleSet.variables` in sorted order. For mixed
                          (unsortable) types, the given order is maintained.
      :type sort_labels: :class:`bool, optional, default=True`
      :param \*\*vectors: Other per-sample data.
      :type \*\*vectors: :class:`array_like`

      :returns: :obj:`.SampleSet`

      .. rubric:: Examples

      >>> bqm = dimod.BinaryQuadraticModel.from_ising({}, {('a', 'b'): -1})
      >>> sampleset = dimod.SampleSet.from_samples_bqm({'a': -1, 'b': 1}, bqm)


   .. py:method:: from_samples_cqm(samples_like, cqm, rtol=1e-06, atol=1e-08, **kwargs)
      :classmethod:

      Build a sample set from raw samples and a constrained quadratic model.

      The constrained quadratic model is used to calculate energies and feasibility.

      :param samples_like: A collection of raw samples. 'samples_like' is an extension of NumPy's array_like.
                           See :func:`.as_samples`.
      :param cqm: A constrained quadratic model.
      :type cqm: :class:`:obj:`.ConstrainedQuadraticModel``
      :param rtol: Relative tolerance for constraint violation.
                   See :meth:`.ConstrainedQuadraticModel.check_feasible` for more information.
      :type rtol: :class:`float, optional, default=1e-6`
      :param atol: Absolute tolerance for constraint violations.
                   See :meth:`.ConstrainedQuadraticModel.check_feasible` for more information.
      :type atol: :class:`float, optional, default=1e-8`
      :param info: Information about the :class:`SampleSet` as a whole formatted as a dict.
      :type info: :class:`dict, optional`
      :param num_occurrences: Number of occurrences for each sample. If not provided, defaults to a vector of 1s.
      :type num_occurrences: :class:`array_like, optional`
      :param aggregate_samples: If True, all samples in returned :obj:`.SampleSet` are unique,
                                with `num_occurrences` accounting for any duplicate samples in
                                `samples_like`.
      :type aggregate_samples: :class:`bool, optional, default=False`
      :param sort_labels: Return :attr:`.SampleSet.variables` in sorted order. For mixed
                          (unsortable) types, the given order is maintained.
      :type sort_labels: :class:`bool, optional, default=True`
      :param \*\*vectors: Other per-sample data.
      :type \*\*vectors: :class:`array_like`

      :returns: :obj:`.SampleSet`

      .. rubric:: Examples

      >>> cqm = dimod.ConstrainedQuadraticModel()
      >>> x, y, z = dimod.Binaries(['x', 'y', 'z'])
      >>> cqm.set_objective(x*y + 2*y*z)
      >>> label = cqm.add_constraint(x*y == 1, label='constraint_1')
      >>> sampleset = dimod.SampleSet.from_samples_cqm({'x': 0, 'y': 1, 'z': 1}, cqm)


   .. py:method:: from_serializable(obj)
      :classmethod:

      Deserialize a :class:`SampleSet`.

      :param obj: A :class:`SampleSet` serialized by :meth:`~.SampleSet.to_serializable`.
      :type obj: :class:`dict`

      :returns: :obj:`.SampleSet`

      .. rubric:: Examples

      This example encodes and decodes using JSON.

      >>> import json
      ...
      >>> samples = dimod.SampleSet.from_samples([-1, 1, -1], dimod.SPIN, energy=-.5)
      >>> s = json.dumps(samples.to_serializable())
      >>> new_samples = dimod.SampleSet.from_serializable(json.loads(s))

      .. seealso:: :meth:`~.SampleSet.to_serializable`


   .. py:method:: indices()
      :property:


   .. py:method:: info()
      :property:

      Dict of information about the :class:`SampleSet` as a whole.

      .. rubric:: Examples

      This example shows the type of information that might be returned by
      a dimod sampler by submitting a BQM that sets a value on a D-Wave
      system's first listed coupler.

      >>> from dwave.system import DWaveSampler    # doctest: +SKIP
      >>> sampler = DWaveSampler()    # doctest: +SKIP
      >>> bqm = dimod.BQM({}, {sampler.edgelist[0]: -1}, 0, dimod.SPIN)   # doctest: +SKIP
      >>> sampler.sample(bqm).info   # doctest: +SKIP
      {'timing': {'qpu_sampling_time': 315,
       'qpu_anneal_time_per_sample': 20,
       'qpu_readout_time_per_sample': 274,
       # Snipped above response for brevity


   .. py:method:: lowest(rtol=1e-05, atol=1e-08)

      Return a sample set containing the lowest-energy samples.

      A sample is included if its energy is within tolerance of the lowest
      energy in the sample set. The following equation is used to determine
      if two values are equivalent:

      absolute(`a` - `b`) <= (`atol` + `rtol` * absolute(`b`))

      See :func:`numpy.isclose` for additional details and caveats.

      :param rtol: The relative tolerance (see above).
      :type rtol: :class:`float, optional, default=1.e-5`
      :param atol: The absolute tolerance (see above).
      :type atol: :class:`float, optional, default=1.e-8`

      :returns: A new sample set containing the lowest energy
                samples as delimited by configured tolerances from the lowest energy
                sample in the current sample set.
      :rtype: :obj:`.SampleSet`

      .. rubric:: Examples

      >>> sampleset = dimod.ExactSolver().sample_ising({'a': .001},
      ...                                              {('a', 'b'): -1})
      >>> print(sampleset.lowest())
         a  b energy num_oc.
      0 -1 -1 -1.001       1
      ['SPIN', 1 rows, 1 samples, 2 variables]
      >>> print(sampleset.lowest(atol=.1))
         a  b energy num_oc.
      0 -1 -1 -1.001       1
      1 +1 +1 -0.999       1
      ['SPIN', 2 rows, 2 samples, 2 variables]

      .. note::

         "Lowest energy" is the lowest energy in the sample set. This is not
         always the "ground energy" which is the lowest energy possible
         for a binary quadratic model.


   .. py:method:: min_samples()
      :property:


   .. py:method:: record()
      :property:

      :obj:`numpy.recarray` containing the samples, energies, number of occurences, and other sample data.

      .. rubric:: Examples

      >>> sampler = dimod.ExactSolver()
      >>> sampleset = sampler.sample_ising({'a': -0.5, 'b': 1.0}, {('a', 'b'): -1.0})
      >>> sampleset.record.sample     # doctest: +SKIP
      array([[-1, -1],
             [ 1, -1],
             [ 1,  1],
             [-1,  1]], dtype=int8)
      >>> len(sampleset.record.energy)
      4


   .. py:method:: relabel_variables(mapping, inplace=True)

      Relabel the variables of a :class:`SampleSet` according to the specified mapping.

      :param mapping: Mapping from current variable labels to new, as a dict. If incomplete mapping is
                      specified, unmapped variables keep their current labels.
      :type mapping: :class:`dict`
      :param inplace: If True, the current :class:`SampleSet` is updated; otherwise, a new
                      :class:`SampleSet` is returned.
      :type inplace: :class:`bool, optional, default=True`

      :returns: SampleSet with relabeled variables. If `inplace` is True, returns
                itself.
      :rtype: :class:`.SampleSet`

      .. rubric:: Notes

      This function is non-blocking unless `inplace==True`, in which case
      the sample set is resolved.

      .. rubric:: Examples

      This example creates a relabeled copy of a :class:`SampleSet`.

      >>> sampleset = dimod.ExactSolver().sample_ising({'a': -0.5, 'b': 1.0}, {('a', 'b'): -1})
      >>> new_sampleset = sampleset.relabel_variables({'a': 0, 'b': 1}, inplace=False)
      >>> new_sampleset.variables
      Variables([0, 1])


   .. py:method:: resolve()

      Ensure that the sampleset is resolved if constructed from a future.



   .. py:method:: samples(n=None, sorted_by='energy')

      Return an iterable over the samples.

      :param n: Maximum number of samples to return in the view.
      :type n: :class:`int, optional, default=None`
      :param sorted_by: Selects the record field used to sort the samples. If None,
                        samples are returned in record order.
      :type sorted_by: :class:`str/None, optional, default='energy'`

      :returns: A view object mapping variable labels to
                values.
      :rtype: :obj:`.SamplesArray`

      .. rubric:: Examples

      >>> sampleset = dimod.ExactSolver().sample_ising({'a': 0.1, 'b': 0.0},
      ...                                              {('a', 'b'): 1})
      >>> for sample in sampleset.samples():   # doctest: +SKIP
      ...     print(sample)
      {'a': -1, 'b': 1}
      {'a': 1, 'b': -1}
      {'a': -1, 'b': -1}
      {'a': 1, 'b': 1}

      >>> sampleset = dimod.ExactSolver().sample_ising({'a': 0.1, 'b': 0.0},
      ...                                              {('a', 'b'): 1})
      >>> samples = sampleset.samples()
      >>> samples[0]
      {'a': -1, 'b': 1}
      >>> samples[0, 'a']
      -1
      >>> samples[0, ['b', 'a']]
      array([ 1, -1], dtype=int8)
      >>> samples[1:, ['a', 'b']]
      array([[ 1, -1],
             [-1, -1],
             [ 1,  1]], dtype=int8)


   .. py:method:: slice(*slice_args, **kwargs)

      Create a new sample set with rows sliced according to standard Python
      slicing syntax.

      :param start: Start index for `slice`.
      :type start: :class:`int, optional, default=None`
      :param stop: Stop index for `slice`.
      :type stop: :class:`int`
      :param step: Step value for `slice`.
      :type step: :class:`int, optional, default=None`
      :param sorted_by: Selects the record field used to sort the samples before
                        slicing. Note that `sorted_by` determines the sample order in
                        the returned sample set.
      :type sorted_by: :class:`str/None, optional, default='energy'`

      :returns: :obj:`.SampleSet`

      .. rubric:: Examples

      >>> import numpy as np
      ...
      >>> sampleset = dimod.SampleSet.from_samples(np.diag(range(1, 11)),
      ...                   dimod.BINARY, energy=range(10))
      >>> print(sampleset)
         0  1  2  3  4  5  6  7  8  9 energy num_oc.
      0  1  0  0  0  0  0  0  0  0  0      0       1
      1  0  1  0  0  0  0  0  0  0  0      1       1
      2  0  0  1  0  0  0  0  0  0  0      2       1
      3  0  0  0  1  0  0  0  0  0  0      3       1
      4  0  0  0  0  1  0  0  0  0  0      4       1
      5  0  0  0  0  0  1  0  0  0  0      5       1
      6  0  0  0  0  0  0  1  0  0  0      6       1
      7  0  0  0  0  0  0  0  1  0  0      7       1
      8  0  0  0  0  0  0  0  0  1  0      8       1
      9  0  0  0  0  0  0  0  0  0  1      9       1
      ['BINARY', 10 rows, 10 samples, 10 variables]

      The above example's first 3 samples by energy == truncate(3):

      >>> print(sampleset.slice(3))
         0  1  2  3  4  5  6  7  8  9 energy num_oc.
      0  1  0  0  0  0  0  0  0  0  0      0       1
      1  0  1  0  0  0  0  0  0  0  0      1       1
      2  0  0  1  0  0  0  0  0  0  0      2       1
      ['BINARY', 3 rows, 3 samples, 10 variables]

      The last 3 samples by energy:

      >>> print(sampleset.slice(-3, None))
         0  1  2  3  4  5  6  7  8  9 energy num_oc.
      0  0  0  0  0  0  0  0  1  0  0      7       1
      1  0  0  0  0  0  0  0  0  1  0      8       1
      2  0  0  0  0  0  0  0  0  0  1      9       1
      ['BINARY', 3 rows, 3 samples, 10 variables]

      Every second sample in between, skipping top and bottom 3:

      >>> print(sampleset.slice(3, -3, 2))
         0  1  2  3  4  5  6  7  8  9 energy num_oc.
      0  0  0  0  1  0  0  0  0  0  0      3       1
      1  0  0  0  0  0  1  0  0  0  0      5       1
      ['BINARY', 2 rows, 2 samples, 10 variables]


   .. py:method:: states()
      :property:


   .. py:method:: to_pandas_dataframe(sample_column=False)

      Convert a sample set to a Pandas DataFrame.

      :param sample_column: If True, samples are
                            represented as a column of type dict.
      :type sample_column: :class:`bool, optional, default=False`

      :returns: :obj:`pandas.DataFrame`.

      .. rubric:: Examples

      >>> samples = dimod.SampleSet.from_samples([{'a': -1, 'b': +1, 'c': -1},
      ...                                         {'a': -1, 'b': -1, 'c': +1}],
      ...                                        dimod.SPIN, energy=-.5)
      >>> samples.to_pandas_dataframe()    # doctest: +SKIP
         a  b  c  energy  num_occurrences
      0 -1  1 -1    -0.5                1
      1 -1 -1  1    -0.5                1
      >>> samples.to_pandas_dataframe(sample_column=True)    # doctest: +SKIP
                             sample  energy  num_occurrences
      0  {'a': -1, 'b': 1, 'c': -1}    -0.5                1
      1  {'a': -1, 'b': -1, 'c': 1}    -0.5                1

      Note that sample sets can be constructed to contain data structures
      incompatible with the target
      `Pandas format <https://pandas.pydata.org/docs>`_.



   .. py:method:: to_serializable(use_bytes=False, bytes_type=bytes, pack_samples=True)

      Convert a :class:`SampleSet` to a serializable object.

      Note that the contents of the :attr:`.SampleSet.info` field are assumed
      to be serializable.

      :param use_bytes: If True, a compact representation of the biases as bytes is used.
      :type use_bytes: :class:`bool, optional, default=False`
      :param bytes_type: If `use_bytes` is True, this class is used to wrap the bytes
                         objects in the serialization. Useful for Python 2 using BSON
                         encoding, which does not accept the raw `bytes` type;
                         `bson.Binary` can be used instead.
      :type bytes_type: :class:`class, optional, default=bytes`
      :param pack_samples: Pack the samples using 1 bit per sample. Samples are never
                           packed when :attr:`SampleSet.vartype` is
                           `~ExtendedVartype.DISCRETE`.
      :type pack_samples: :class:`bool, optional, default=True`

      :returns: Object that can be serialized.
      :rtype: dict

      .. rubric:: Examples

      This example encodes using JSON.

      >>> import json
      ...
      >>> samples = dimod.SampleSet.from_samples([-1, 1, -1], dimod.SPIN, energy=-.5)
      >>> s = json.dumps(samples.to_serializable())

      .. seealso:: :meth:`~.SampleSet.from_serializable`


   .. py:method:: truncate(n, sorted_by='energy')

      Create a new sample set with up to n rows.

      :param n: Maximum number of rows in the returned sample set. Does not return
                any rows above this limit in the original sample set.
      :type n: :class:`int`
      :param sorted_by: Selects the record field used to sort the samples before
                        truncating. Note that this sort order is maintained in the
                        returned sample set.
      :type sorted_by: :class:`str/None, optional, default='energy'`

      :returns: :obj:`.SampleSet`

      .. rubric:: Examples

      >>> import numpy as np
      ...
      >>> sampleset = dimod.SampleSet.from_samples(np.ones((5, 5)), dimod.SPIN, energy=5)
      >>> print(sampleset)
         0  1  2  3  4 energy num_oc.
      0 +1 +1 +1 +1 +1      5       1
      1 +1 +1 +1 +1 +1      5       1
      2 +1 +1 +1 +1 +1      5       1
      3 +1 +1 +1 +1 +1      5       1
      4 +1 +1 +1 +1 +1      5       1
      ['SPIN', 5 rows, 5 samples, 5 variables]
      >>> print(sampleset.truncate(2))
         0  1  2  3  4 energy num_oc.
      0 +1 +1 +1 +1 +1      5       1
      1 +1 +1 +1 +1 +1      5       1
      ['SPIN', 2 rows, 2 samples, 5 variables]

      See:
          :meth:`SampleSet.slice`



   .. py:method:: variables()
      :property:

      :class:`~.variables.Variables` of variable labels.

      Corresponds to columns of the sample field of :attr:`.SampleSet.record`.


   .. py:method:: vartype()
      :property:

      :class:`.Vartype` of the samples.



.. py:class:: SASampler(beta_min: Optional[float] = None, beta_max: Optional[float] = None, num_sweeps: Optional[int] = None, num_reads: Optional[int] = None, schedule: Optional[list] = None)

   Bases: :py:obj:`openjij.sampler.sampler.BaseSampler`

   .. autoapi-inheritance-diagram:: openjij.sampler.SASampler
      :parts: 1

   Sampler with Simulated Annealing (SA).

   :param beta_min: Minmum beta (inverse temperature).
                    You can overwrite in methods .sample_*.
   :type beta_min: :class:`float`
   :param beta_max: Maximum beta (inverse temperature).
                    You can overwrite in methods .sample_*.
   :type beta_max: :class:`float`
   :param num_reads: number of sampling (algorithm) runs. defaults None.
                     You can overwrite in methods .sample_*.
   :type num_reads: :class:`int`
   :param num_sweeps: number of MonteCarlo steps during SA. defaults None.
                      You can overwrite in methods .sample_*.
   :type num_sweeps: :class:`int`
   :param schedule_info: Information about an annealing schedule.
   :type schedule_info: :class:`dict`

   :raises ValueError: If schedules or variables violate as below.
   :raises - not list or numpy.array.:
   :raises - not list of tuple (beta: float, step_length : int).
   :raises - beta is less than zero.:

   .. py:attribute:: properties
      

      

   .. py:method:: parameters()
      :property:

      Parameters as a dict, where keys are keyword parameters accepted by the
      sampler methods and values are lists of the properties relevent to each
      parameter.


   .. py:method:: remove_unknown_kwargs(**kwargs) -> Dict[str, Any]

      Remove with warnings any keyword arguments not accepted by the sampler.

      :param \*\*kwargs: Keyword arguments to be validated.

      Returns: Updated `kwargs` dict.

      .. rubric:: Examples

      >>> import warnings
      >>> sampler = dimod.RandomSampler()
      >>> with warnings.catch_warnings():
      ...     warnings.filterwarnings('ignore')
      ...     try:
      ...         sampler.remove_unknown_kwargs(num_reads=10, non_param=3)
      ...     except dimod.exceptions.SamplerUnknownArgWarning:
      ...        pass
      {'num_reads': 10}


   .. py:method:: sample(bqm: Union[openj.model.model.BinaryQuadraticModel, dimod.BinaryQuadraticModel], beta_min: Optional[float] = None, beta_max: Optional[float] = None, num_sweeps: Optional[int] = None, num_reads: Optional[int] = None, schedule: Optional[list] = None, initial_state: Optional[Union[list, dict]] = None, updater: Optional[str] = None, sparse: Optional[bool] = None, reinitialize_state: Optional[bool] = None, seed: Optional[int] = None) -> openjij.sampler.response.Response

      Sample Ising model.

      :param bqm:
      :type bqm: :class:`openjij.model.model.BinaryQuadraticModel`
      :param beta_min: minimal value of inverse temperature
      :type beta_min: :class:`float`
      :param beta_max: maximum value of inverse temperature
      :type beta_max: :class:`float`
      :param num_sweeps: number of sweeps
      :type num_sweeps: :class:`int`
      :param num_reads: number of reads
      :type num_reads: :class:`int`
      :param schedule: list of inverse temperature
      :type schedule: :class:`list`
      :param initial_state: initial state
      :type initial_state: :class:`dict`
      :param updater: updater algorithm
      :type updater: :class:`str`
      :param reinitialize_state: if true reinitialize state for each run
      :type reinitialize_state: :class:`bool`
      :param seed: seed for Monte Carlo algorithm
      :type seed: :class:`int`

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`

      .. rubric:: Examples

      for Ising case::

          >>> h = {0: -1, 1: -1, 2: 1, 3: 1}
          >>> J = {(0, 1): -1, (3, 4): -1}
          >>> sampler = openj.SASampler()
          >>> res = sampler.sample_ising(h, J)

      for QUBO case::

          >>> Q = {(0, 0): -1, (1, 1): -1, (2, 2): 1, (3, 3): 1, (4, 4): 1, (0, 1): -1, (3, 4): 1}
          >>> sampler = openj.SASampler()
          >>> res = sampler.sample_qubo(Q)


   .. py:method:: sample_hubo(J: Union[dict, openj.model.model.BinaryPolynomialModel, cimod.BinaryPolynomialModel], vartype: Optional[str] = None, beta_min: Optional[float] = None, beta_max: Optional[float] = None, num_sweeps: Optional[int] = None, num_reads: Optional[int] = None, schedule: Optional[list] = None, initial_state: Optional[Union[list, dict]] = None, updater: Optional[str] = None, reinitialize_state: Optional[bool] = None, seed: Optional[int] = None) -> openjij.sampler.response.Response

      Sampling from higher order unconstrainted binary optimization.

      :param J: Interactions.
      :type J: :class:`dict`
      :param vartype: "SPIN" or "BINARY".
      :type vartype: :class:`str, openjij.VarType`
      :param beta_min: Minimum beta (initial inverse temperature). Defaults to None.
      :type beta_min: :class:`float, optional`
      :param beta_max: Maximum beta (final inverse temperature). Defaults to None.
      :type beta_max: :class:`float, optional`
      :param schedule: schedule list. Defaults to None.
      :type schedule: :class:`list, optional`
      :param num_sweeps: number of sweeps. Defaults to None.
      :type num_sweeps: :class:`int, optional`
      :param num_reads: number of reads. Defaults to 1.
      :type num_reads: :class:`int, optional`
      :param init_state: initial state. Defaults to None.
      :type init_state: :class:`list, optional`
      :param reinitialize_state: if true reinitialize state for each run
      :type reinitialize_state: :class:`bool`
      :param seed: seed for Monte Carlo algorithm. Defaults to None.
      :type seed: :class:`int, optional`

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`

      Examples::
          for Ising case::
              >>> sampler = openjij.SASampler()
              >>> J = {(0,): -1, (0, 1): -1, (0, 1, 2): 1}
              >>> response = sampler.sample_hubo(J, "SPIN")

          for Binary case::
              >>> sampler = ooenjij.SASampler()
              >>> J = {(0,): -1, (0, 1): -1, (0, 1, 2): 1}
              >>> response = sampler.sample_hubo(J, "BINARY")


   .. py:method:: sample_ising(h, J, **parameters)

      Sample from an Ising model using the implemented sample method.

      :param h: Linear biases
      :type h: :class:`dict`
      :param J: Quadratic biases
      :type J: :class:`dict`

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`


   .. py:method:: sample_qubo(Q, **parameters)

      Sample from a QUBO model using the implemented sample method.

      :param Q: Coefficients of a quadratic unconstrained binary optimization
      :type Q: :class:`dict or numpy.ndarray`

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`



.. py:class:: SQASampler(beta: Optional[float] = None, gamma: Optional[float] = None, num_sweeps: Optional[int] = None, num_reads: Optional[int] = None, schedule: Optional[list] = None, trotter: Optional[int] = None)

   Bases: :py:obj:`openjij.sampler.sampler.BaseSampler`

   .. autoapi-inheritance-diagram:: openjij.sampler.SQASampler
      :parts: 1

   Sampler with Simulated Quantum Annealing (SQA).

   Inherits from :class:`openjij.sampler.sampler.BaseSampler`.
   Hamiltonian

   .. math::

       H(s) = s H_p + \Gamma (1-s)\sum_i \sigma_i^x

   where :math:`H_p` is the problem Hamiltonian we want to solve.

   :param beta: Inverse temperature.
   :type beta: :class:`float`
   :param gamma: Amplitude of quantum fluctuation.
   :type gamma: :class:`float`
   :param trotter: Trotter number.
   :type trotter: :class:`int`
   :param num_sweeps: number of sweeps
   :type num_sweeps: :class:`int`
   :param schedule: schedule list
   :type schedule: :class:`list`
   :param num_reads: Number of iterations.
   :type num_reads: :class:`int`
   :param schedule_info: Information about a annealing schedule.
   :type schedule_info: :class:`dict`

   :raises ValueError: If the schedule violates as below.
   :raises - not list or numpy.array.:
   :raises - schedule range is '0 <= s <= 1'.:

   .. py:attribute:: properties
      

      

   .. py:method:: parameters()
      :property:

      Parameters as a dict, where keys are keyword parameters accepted by the
      sampler methods and values are lists of the properties relevent to each
      parameter.


   .. py:method:: remove_unknown_kwargs(**kwargs) -> Dict[str, Any]

      Remove with warnings any keyword arguments not accepted by the sampler.

      :param \*\*kwargs: Keyword arguments to be validated.

      Returns: Updated `kwargs` dict.

      .. rubric:: Examples

      >>> import warnings
      >>> sampler = dimod.RandomSampler()
      >>> with warnings.catch_warnings():
      ...     warnings.filterwarnings('ignore')
      ...     try:
      ...         sampler.remove_unknown_kwargs(num_reads=10, non_param=3)
      ...     except dimod.exceptions.SamplerUnknownArgWarning:
      ...        pass
      {'num_reads': 10}


   .. py:method:: sample(bqm: Union[openjij.model.model.BinaryQuadraticModel, dimod.BinaryQuadraticModel], beta: Optional[float] = None, gamma: Optional[float] = None, num_sweeps: Optional[int] = None, schedule: Optional[list] = None, trotter: Optional[int] = None, num_reads: Optional[int] = None, initial_state: Optional[Union[list, dict]] = None, updater: Optional[str] = None, sparse: Optional[bool] = None, reinitialize_state: Optional[bool] = None, seed: Optional[int] = None) -> openjij.sampler.response.Response

      Sampling from the Ising model.

      :param bqm:
      :type bqm: :class:`openjij.BinaryQuadraticModel`
      :param beta: inverse tempareture.
      :type beta: :class:`float, optional`
      :param gamma: strangth of transverse field. Defaults to None.
      :type gamma: :class:`float, optional`
      :param num_sweeps: number of sweeps. Defaults to None.
      :type num_sweeps: :class:`int, optional`
      :param schedule: List of annealing parameter. Defaults to None.
      :type schedule: :class:`list[list[float, int]], optional`
      :param trotter: Trotter number.
      :type trotter: :class:`int`
      :param num_reads: number of sampling. Defaults to 1.
      :type num_reads: :class:`int, optional`
      :param initial_state: Initial state. Defaults to None.
      :type initial_state: :class:`list[int], optional`
      :param updater: update method. Defaults to 'single spin flip'.
      :type updater: :class:`str, optional`
      :param reinitialize_state: Re-initilization at each sampling. Defaults to True.
      :type reinitialize_state: :class:`bool, optional`
      :param seed: Sampling seed. Defaults to None.
      :type seed: :class:`int, optional`

      :raises ValueError:

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`

      .. rubric:: Examples

      for Ising case::

          >>> h = {0: -1, 1: -1, 2: 1, 3: 1}
          >>> J = {(0, 1): -1, (3, 4): -1}
          >>> sampler = openjij.SQASampler()
          >>> res = sampler.sample_ising(h, J)

      for QUBO case::

          >>> Q = {(0, 0): -1, (1, 1): -1, (2, 2): 1, (3, 3): 1, (4, 4): 1, (0, 1): -1, (3, 4): 1}
          >>> sampler = openjij.SQASampler()
          >>> res = sampler.sample_qubo(Q)


   .. py:method:: sample_ising(h, J, **parameters)

      Sample from an Ising model using the implemented sample method.

      :param h: Linear biases
      :type h: :class:`dict`
      :param J: Quadratic biases
      :type J: :class:`dict`

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`


   .. py:method:: sample_qubo(Q, **parameters)

      Sample from a QUBO model using the implemented sample method.

      :param Q: Coefficients of a quadratic unconstrained binary optimization
      :type Q: :class:`dict or numpy.ndarray`

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`



.. py:function:: measure_time(func)

   Decorator for measuring calculation time.

   :param func: decorator function


