:py:mod:`openjij.utils`
=======================

.. py:module:: openjij.utils


Submodules
----------
.. toctree::
   :titlesonly:
   :maxdepth: 1

   benchmark/index.rst
   decorator/index.rst
   graph_utils/index.rst
   res_convertor/index.rst
   time_measure/index.rst


Package Contents
----------------


Functions
~~~~~~~~~

.. autoapisummary::

   openjij.utils.convert_response
   openjij.utils.residual_energy
   openjij.utils.se_lower_tts
   openjij.utils.se_residual_energy
   openjij.utils.se_success_probability
   openjij.utils.se_upper_tts
   openjij.utils.solver_benchmark
   openjij.utils.success_probability
   openjij.utils.time_to_solution



.. py:function:: convert_response(response)


.. py:function:: residual_energy(response, ref_energy)

   Calculate redisual energy from measure energy
   :param response: response from solver (or sampler).
   :type response: openjij.Response
   :param ref_energy: the reference energy (usually use the ground energy)
   :type ref_energy: float

   :returns: Residual energy which is defined as :math:`\langle E \rangle - E_0` (:math:`\langle...\rangle` represents average, :math:`E_0` is the reference energy (usually use the ground energy)).
   :rtype: float


.. py:function:: se_lower_tts(tts, success_prob, computation_time, p_r, se_success_prob)

   :param success_prob: success probability.
   :type success_prob: float
   :param computation_time:
   :type computation_time: float
   :param p_r: thereshold probability to calculate time to solution.
   :type p_r: float

   :returns: time to solution :math:`\tau * \log(1-pr)/\log(1-ps)` 's standard error which pr is thereshold probability, ps is success probability and :math:`tau` is computation time.
   :rtype: float


.. py:function:: se_residual_energy(response, ref_energy)

   Calculate redisual energy's standard error from measure energy
   :param response: response from solver (or sampler).
   :type response: openjij.Response
   :param ref_energy: the reference energy (usually use the ground energy)
   :type ref_energy: float

   :returns: redisual energy's standard error from measure energy
   :rtype: float


.. py:function:: se_success_probability(response, solutions, ref_energy=0, measure_with_energy=False)

   Calculate success probability's standard error from openjij.response
   :param response: response from solver (or sampler).
   :type response: openjij.Response
   :param solutions: true solutions.
   :type solutions: list[int]

   :returns: Success probability's standard error.

             * When measure_with_energy is False, success is defined as getting the same state as solutions.
             * When measure_with_energy is True, success is defined as getting a state which energy is below reference energy
   :rtype: float


.. py:function:: se_upper_tts(tts, success_prob, computation_time, p_r, se_success_prob)

   :param success_prob: success probability.
   :type success_prob: float
   :param computation_time:
   :type computation_time: float
   :param p_r: thereshold probability to calculate time to solution.
   :type p_r: float

   Returens:
       float: time to solution :math:`\tau * \log(1-pr)/\log(1-ps)` 's standard error which pr is thereshold probability, ps is success probability and :math:`tau` is computation time.


.. py:function:: solver_benchmark(solver, time_list, solutions=[], args={}, p_r=0.99, ref_energy=0, measure_with_energy=False, time_name='execution_time')

   Calculate 'success probability', 'TTS', 'Residual energy','Standard Error' with computation time
   :param solver: returns openjij.Response, and solver has arguments 'time' and '**args'
   :type solver: callable
   :param time_list:
   :type time_list: list
   :param solutions: true solution or list of solution (if solutions are degenerated).
   :type solutions: list(list(int)), list(int)
   :param args: Arguments for solver.
   :type args: dict
   :param p_r: Thereshold probability for time to solutions.
   :type p_r: float
   :param ref_energy: The ground (reference to calculate success probability and the residual energy) energy.
   :type ref_energy: float
   :param measure_with_energy: use a energy as measure for success
   :type measure_with_energy: bool

   :returns: dictionary which has the following keys:

             * **time**: list of compuation time
             * **success_prob** list of success probability at each computation time
             * **tts**: list of time to solusion at each computation time
             * **residual_energy**: list of residual energy at each computation time
             * **se_lower_tts**: list of tts's lower standard error at each computation time
             * **se_upper_tts**: list of tts's upper standard error at each computation time
             * **se_success_prob**: list of success probability's standard error at each computation time
             * **se_residual_energy**: list of residual_energy's standard error at each computation time
             * **info** (dict): Parameter information for the benchmark
   :rtype: dict


.. py:function:: success_probability(response, solutions, ref_energy=0, measure_with_energy=False)

   Calculate success probability from openjij.response
   :param response: response from solver (or sampler).
   :type response: openjij.Response
   :param solutions: true solutions.
   :type solutions: list[int]

   :returns: Success probability.

             * When measure_with_energy is False, success is defined as getting the same state as solutions.
             * When measure_with_energy is True, success is defined as getting a state which energy is below reference energy
   :rtype: float


.. py:function:: time_to_solution(success_prob, computation_time, p_r)

   :param success_prob: success probability.
   :type success_prob: float
   :param computation_time:
   :type computation_time: float
   :param p_r: thereshold probability to calculate time to solution.
   :type p_r: float

   :returns: time to solution :math:`\tau * \log(1-pr)/\log(1-ps)` which pr is thereshold probability, ps is success probability and :math:`tau` is computation time.
   :rtype: float


