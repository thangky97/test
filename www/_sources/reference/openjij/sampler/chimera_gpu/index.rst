:py:mod:`openjij.sampler.chimera_gpu`
=====================================

.. py:module:: openjij.sampler.chimera_gpu


Submodules
----------
.. toctree::
   :titlesonly:
   :maxdepth: 1

   base_gpu_chimera/index.rst
   gpu_sa_sampler/index.rst
   gpu_sqa_sampler/index.rst


Package Contents
----------------

Classes
~~~~~~~

.. autoapisummary::

   openjij.sampler.chimera_gpu.GPUChimeraSASampler
   openjij.sampler.chimera_gpu.GPUChimeraSQASampler




.. py:class:: GPUChimeraSASampler(beta_min=None, beta_max=None, num_sweeps=1000, schedule=None, num_reads=1, unit_num_L=None)

   Bases: :py:obj:`openjij.sampler.sa_sampler.SASampler`, :py:obj:`openjij.sampler.chimera_gpu.base_gpu_chimera.BaseGPUChimeraSampler`

   .. autoapi-inheritance-diagram:: openjij.sampler.chimera_gpu.GPUChimeraSASampler
      :parts: 1

   Sampler with Simulated Annealing (SA) on GPU.

   Inherits from :class:`openjij.sampler.sampler.BaseSampler`.

   :param beta_min: Minimum inverse temperature.
   :type beta_min: :class:`float`
   :param beta_max: Maximum inverse temperature.
   :type beta_max: :class:`float`
   :param num_sweeps: Length of Monte Carlo step.
   :type num_sweeps: :class:`int`
   :param schedule_info: Information about a annealing schedule.
   :type schedule_info: :class:`dict`
   :param num_reads: Number of iterations.
   :type num_reads: :class:`int`
   :param unit_num_L: Length of one side of two-dimensional lattice in which chimera unit cells are arranged.
   :type unit_num_L: :class:`int`

   :raises ValueError: If variables violate as below.
   :raises - trotter number is odd.:
   :raises - no input "unit_num_L" to an argument or this constructor.:
   :raises - given problem graph is incompatible with chimera graph.:
   :raises AttributeError: If GPU doesn't work.

   .. py:attribute:: properties
      

      

   .. py:method:: adjacency() -> Dict[dimod.typing.Variable, Set]
      :property:

      Adjacency structure formatted as a dict, where keys are the nodes of
      the structured sampler and values are sets of all adjacent nodes for each
      key node.


   .. py:method:: edgelist()
      :property:

      Edges/interactions allowed by the sampler.



   .. py:method:: nodelist()
      :property:

      Nodes/variables allowed by the sampler.


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


   .. py:method:: sample_ising(h, J, beta_min=None, beta_max=None, num_sweeps=None, num_reads=1, schedule=None, initial_state=None, updater=None, reinitialize_state=True, seed=None, unit_num_L=None)

      Sample with Ising model.

      :param h: linear biases
      :type h: :class:`dict`
      :param J: quadratic biases
      :type J: :class:`dict`
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
      :param unit_num_L: number of chimera units
      :type unit_num_L: :class:`int`

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`

      Examples::

          >>> sampler = openjij.sampler.chimera_gpu.gpu_sa_sampler.GPUChimeraSASampler(unit_num_L=2)
          >>> h = {0: -1, 1: -1, 2: 1, 3: 1},
          >>> J = {(0, 4): -1, (2, 5): -1}
          >>> res = sampler.sample_ising(h, J)


   .. py:method:: sample_qubo(Q, **parameters)

      Sample from a QUBO model using the implemented sample method.

      :param Q: Coefficients of a quadratic unconstrained binary optimization
      :type Q: :class:`dict or numpy.ndarray`

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`


   .. py:method:: structure() -> _Structure
      :property:

      Structure of the structured sampler formatted as a
      :func:`~collections.namedtuple` where the 3-tuple values are the
      :attr:`.nodelist`, :attr:`.edgelist` and :attr:`.adjacency` attributes.


   .. py:method:: to_networkx_graph()

      Convert structure to NetworkX graph format.

      Note that NetworkX must be installed for this method to work.

      :returns: A NetworkX graph containing the nodes and
                edges from the sampler's structure.
      :rtype: :class:`networkx.Graph`


   .. py:method:: valid_bqm_graph(bqm: dimod.BinaryQuadraticModel) -> bool

      Validate that problem defined by :class:`dimod.BinaryQuadraticModel`
      matches the graph provided by the sampler.

      :param bqm: :class:`dimod.BinaryQuadraticModel` object to validate.

      :returns: Boolean indicating validity of BQM graph compared to sampler graph.



.. py:class:: GPUChimeraSQASampler(beta=10.0, gamma=1.0, trotter=4, num_sweeps=100, schedule=None, num_reads=1, unit_num_L=None)

   Bases: :py:obj:`openjij.sampler.sqa_sampler.SQASampler`, :py:obj:`openjij.sampler.chimera_gpu.base_gpu_chimera.BaseGPUChimeraSampler`

   .. autoapi-inheritance-diagram:: openjij.sampler.chimera_gpu.GPUChimeraSQASampler
      :parts: 1

   Sampler with Simulated Quantum Annealing (SQA) on GPU.

   Inherits from :class:`openjij.sampler.sqa_sampler.SQASampler`.

   :param beta: Inverse temperature.
   :type beta: :class:`float`
   :param gamma: Amplitude of quantum fluctuation.
   :type gamma: :class:`float`
   :param trotter: Trotter number.
   :type trotter: :class:`int`
   :param num_sweeps: number of sweeps
   :type num_sweeps: :class:`int`
   :param schedule_info: Information about a annealing schedule.
   :type schedule_info: :class:`dict`
   :param num_reads: Number of iterations.
   :type num_reads: :class:`int`
   :param unit_num_L: Length of one side of two-dimensional lattice in which chimera unit cells are arranged.
   :type unit_num_L: :class:`int`

   :raises ValueError: If variables violate as below.
   :raises - trotter number is odd.:
   :raises - no input "unit_num_L" to an argument or this constructor.:
   :raises - given problem graph is incompatible with chimera graph.:
   :raises AttributeError: If GPU doesn't work.

   .. py:attribute:: properties
      

      

   .. py:method:: adjacency() -> Dict[dimod.typing.Variable, Set]
      :property:

      Adjacency structure formatted as a dict, where keys are the nodes of
      the structured sampler and values are sets of all adjacent nodes for each
      key node.


   .. py:method:: edgelist()
      :property:

      Edges/interactions allowed by the sampler.



   .. py:method:: nodelist()
      :property:

      Nodes/variables allowed by the sampler.


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


   .. py:method:: sample_ising(h, J, beta=None, gamma=None, num_sweeps=None, schedule=None, num_reads=None, unit_num_L=None, initial_state=None, updater=None, reinitialize_state=True, seed=None)

      Sampling from the Ising model.

      :param h: Linear term of the target Ising model.
      :type h: :class:`dict`
      :param J: Quadratic term of the target Ising model.
      :type J: :class:`dict`
      :param beta: inverse tempareture.
      :type beta: :class:`float, optional`
      :param gamma: strangth of transverse field. Defaults to None.
      :type gamma: :class:`float, optional`
      :param num_sweeps: number of sweeps. Defaults to None.
      :type num_sweeps: :class:`int, optional`
      :param schedule: List of annealing parameter. Defaults to None.
      :type schedule: :class:`list[list[float, int]], optional`
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

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`

      Examples::

          >>> sampler = openjij.sampler.chimera_gpu.gpu_sqa_sampler.GPUChimeraSQASampler(unit_num_L=2)
          >>> h = {0: -1, 1: -1, 2: 1, 3: 1},
          >>> J = {(0, 4): -1, (2, 5): -1}
          >>> res = sampler.sample_ising(h, J)


   .. py:method:: sample_qubo(Q, **parameters)

      Sample from a QUBO model using the implemented sample method.

      :param Q: Coefficients of a quadratic unconstrained binary optimization
      :type Q: :class:`dict or numpy.ndarray`

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`


   .. py:method:: structure() -> _Structure
      :property:

      Structure of the structured sampler formatted as a
      :func:`~collections.namedtuple` where the 3-tuple values are the
      :attr:`.nodelist`, :attr:`.edgelist` and :attr:`.adjacency` attributes.


   .. py:method:: to_networkx_graph()

      Convert structure to NetworkX graph format.

      Note that NetworkX must be installed for this method to work.

      :returns: A NetworkX graph containing the nodes and
                edges from the sampler's structure.
      :rtype: :class:`networkx.Graph`


   .. py:method:: valid_bqm_graph(bqm: dimod.BinaryQuadraticModel) -> bool

      Validate that problem defined by :class:`dimod.BinaryQuadraticModel`
      matches the graph provided by the sampler.

      :param bqm: :class:`dimod.BinaryQuadraticModel` object to validate.

      :returns: Boolean indicating validity of BQM graph compared to sampler graph.



