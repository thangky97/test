:py:mod:`openjij.sampler.sampler`
=================================

.. py:module:: openjij.sampler.sampler

.. autoapi-nested-parse::

   This module defines the abstract sampler (BaseSampler).



Module Contents
---------------

Classes
~~~~~~~

.. autoapisummary::

   openjij.sampler.sampler.BaseSampler



Functions
~~~~~~~~~

.. autoapisummary::

   openjij.sampler.sampler.measure_time



.. py:class:: BaseSampler

   Bases: :py:obj:`dimod.Sampler`

   .. autoapi-inheritance-diagram:: openjij.sampler.sampler.BaseSampler
      :parts: 1

   Base sampler class of python wrapper for cxxjij simulator.

   .. py:attribute:: parameters
      

      

   .. py:attribute:: properties
      

      

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


   .. py:method:: sample(bqm, **parameters)

      Sample from a binary quadratic model.

      :param bqm: Binary Qudratic Model
      :type bqm: :class:`openjij.BinaryQuadraticModel`
      :param \*\*parameters: See the implemented sampling for additional keyword definitions.

      :returns: results
      :rtype: :class:`openjij.sampler.response.Response`


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


