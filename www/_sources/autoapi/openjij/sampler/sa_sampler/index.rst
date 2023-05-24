:py:mod:`openjij.sampler.sa_sampler`
====================================

.. py:module:: openjij.sampler.sa_sampler


Module Contents
---------------

Classes
~~~~~~~

.. autoapisummary::

   openjij.sampler.sa_sampler.SASampler



Functions
~~~~~~~~~

.. autoapisummary::

   openjij.sampler.sa_sampler.geometric_hubo_beta_schedule
   openjij.sampler.sa_sampler.geometric_ising_beta_schedule



.. py:class:: SASampler(beta_min: Optional[float] = None, beta_max: Optional[float] = None, num_sweeps: Optional[int] = None, num_reads: Optional[int] = None, schedule: Optional[list] = None)

   Bases: :py:obj:`openjij.sampler.sampler.BaseSampler`

   .. autoapi-inheritance-diagram:: openjij.sampler.sa_sampler.SASampler
      :parts: 1

   Sampler with Simulated Annealing (SA).

   :param beta_min: Minmum beta (inverse temperature).
                    You can overwrite in methods .sample_*.
   :type beta_min: float
   :param beta_max: Maximum beta (inverse temperature).
                    You can overwrite in methods .sample_*.
   :type beta_max: float
   :param num_reads: number of sampling (algorithm) runs. defaults None.
                     You can overwrite in methods .sample_*.
   :type num_reads: int
   :param num_sweeps: number of MonteCarlo steps during SA. defaults None.
                      You can overwrite in methods .sample_*.
   :type num_sweeps: int
   :param schedule_info: Information about an annealing schedule.
   :type schedule_info: dict

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

      sample Ising model.

      :param bqm:
      :type bqm: openjij.model.model.BinaryQuadraticModel
      :param beta_min: minimal value of inverse temperature
      :type beta_min: float
      :param beta_max: maximum value of inverse temperature
      :type beta_max: float
      :param num_sweeps: number of sweeps
      :type num_sweeps: int
      :param num_reads: number of reads
      :type num_reads: int
      :param schedule: list of inverse temperature
      :type schedule: list
      :param initial_state: initial state
      :type initial_state: dict
      :param updater: updater algorithm
      :type updater: str
      :param reinitialize_state: if true reinitialize state for each run
      :type reinitialize_state: bool
      :param seed: seed for Monte Carlo algorithm
      :type seed: int

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

      sampling from higher order unconstrainted binary optimization.

      :param J: Interactions.
      :type J: dict
      :param vartype: "SPIN" or "BINARY".
      :type vartype: str, openjij.VarType
      :param beta_min: Minimum beta (initial inverse temperature). Defaults to None.
      :type beta_min: float, optional
      :param beta_max: Maximum beta (final inverse temperature). Defaults to None.
      :type beta_max: float, optional
      :param schedule: schedule list. Defaults to None.
      :type schedule: list, optional
      :param num_sweeps: number of sweeps. Defaults to None.
      :type num_sweeps: int, optional
      :param num_reads: number of reads. Defaults to 1.
      :type num_reads: int, optional
      :param init_state: initial state. Defaults to None.
      :type init_state: list, optional
      :param reinitialize_state: if true reinitialize state for each run
      :type reinitialize_state: bool
      :param seed: seed for Monte Carlo algorithm. Defaults to None.
      :type seed: int, optional

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
      :type h: dict
      :param J: Quadratic biases
      :type J: dict

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`


   .. py:method:: sample_qubo(Q, **parameters)

      Sample from a QUBO model using the implemented sample method.

      :param Q: Coefficients of a quadratic unconstrained binary optimization
      :type Q: dict or numpy.ndarray

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`



.. py:function:: geometric_hubo_beta_schedule(sa_system, beta_max, beta_min, num_sweeps)


.. py:function:: geometric_ising_beta_schedule(model: openjij.model.model.BinaryQuadraticModel, beta_max=None, beta_min=None, num_sweeps=1000)

   make geometric cooling beta schedule

   :param model:
   :type model: openjij.model.BinaryQuadraticModel
   :param beta_max: [description]. Defaults to None.
   :type beta_max: float, optional
   :param beta_min: [description]. Defaults to None.
   :type beta_min: float, optional
   :param num_sweeps: [description]. Defaults to 1000.
   :type num_sweeps: int, optional

   :returns: list of cxxjij.utility.ClassicalSchedule, list of beta range [max, min]


