:py:mod:`openjij.sampler.csqa_sampler`
======================================

.. py:module:: openjij.sampler.csqa_sampler


Module Contents
---------------

Classes
~~~~~~~

.. autoapisummary::

   openjij.sampler.csqa_sampler.CSQASampler




.. py:class:: CSQASampler(beta=5.0, gamma=1.0, num_sweeps=1000, schedule=None, num_reads=1)

   Bases: :py:obj:`openjij.sampler.sqa_sampler.SQASampler`

   .. autoapi-inheritance-diagram:: openjij.sampler.csqa_sampler.CSQASampler
      :parts: 1

   Sampler with continuous-time simulated quantum annealing (CSQA) using Hamiltonian

   .. math::

       H(s) = s H_p + \Gamma (1-s)\sum_i \sigma_i^x

   where :math:`H_p` is the problem Hamiltonian we want to solve.

   :param beta: Inverse temperature.
   :type beta: float
   :param gamma: Amplitude of quantum fluctuation.
   :type gamma: float
   :param schedule: schedule list
   :type schedule: list
   :param step_num: Number of Monte Carlo step.
   :type step_num: int
   :param schedule_info: Information about a annealing schedule.
   :type schedule_info: dict
   :param num_reads: Number of iterations.
   :type num_reads: int
   :param num_sweeps: number of sweeps
   :type num_sweeps: int
   :param schedule_info: Information about a annealing schedule.
   :type schedule_info: dict

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

      Sampling from the Ising model

      :param bqm:
      :type bqm: openjij.BinaryQuadraticModel
      :param beta: inverse tempareture.
      :type beta: float, optional
      :param gamma: strangth of transverse field. Defaults to None.
      :type gamma: float, optional
      :param num_sweeps: number of sweeps. Defaults to None.
      :type num_sweeps: int, optional
      :param schedule: List of annealing parameter. Defaults to None.
      :type schedule: list[list[float, int]], optional
      :param trotter: Trotter number.
      :type trotter: int
      :param num_reads: number of sampling. Defaults to 1.
      :type num_reads: int, optional
      :param initial_state: Initial state. Defaults to None.
      :type initial_state: list[int], optional
      :param updater: update method. Defaults to 'single spin flip'.
      :type updater: str, optional
      :param reinitialize_state: Re-initilization at each sampling. Defaults to True.
      :type reinitialize_state: bool, optional
      :param seed: Sampling seed. Defaults to None.
      :type seed: int, optional

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
      :type h: dict
      :param J: quadratic biases
      :type J: dict
      :param beta: inverse temperature
      :type beta: float, optional
      :param gamma: strength of transverse field
      :type gamma: float, optional
      :param num_sweeps: number of sampling.
      :type num_sweeps: int, optional
      :param schedule: schedule list
      :type schedule: list, optional
      :param num_reads: number of iterations
      :type num_reads: int, optional
      :param initial_state: initial state of spins
      :type initial_state: optional
      :param updater: updater algorithm
      :type updater: str, optional
      :param reinitialize_state: Re-initilization at each sampling. Defaults to True.
      :type reinitialize_state: bool, optional
      :param seed: Sampling seed.
      :type seed: int, optional

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
      :type Q: dict or numpy.ndarray

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`



