:py:mod:`openjij.model.model`
=============================

.. py:module:: openjij.model.model

.. autoapi-nested-parse::

   | This module defines the BinaryQuadraticModel with the Hamiltonian,

   .. math::

       H = \sum_{i\neq j} J_{ij}\sigma_i \sigma_j + \sum_{i} h_{i}\sigma_i,

   | in an Ising form and

   .. math::

       H = \sum_{ij} Q_{ij}x_i x_j + \sum_{i} H_{i}x_i,

   | in a QUBO form.
   | The methods and usage are basically the same as `dimod <https://github.com/dwavesystems/dimod>`_.



Module Contents
---------------


Functions
~~~~~~~~~

.. autoapisummary::

   openjij.model.model.BinaryPolynomialModel
   openjij.model.model.BinaryQuadraticModel
   openjij.model.model.bqm_from_numpy_matrix
   openjij.model.model.make_BinaryPolynomialModel
   openjij.model.model.make_BinaryPolynomialModel_from_JSON
   openjij.model.model.make_BinaryPolynomialModel_from_hising
   openjij.model.model.make_BinaryPolynomialModel_from_hubo
   openjij.model.model.make_BinaryQuadraticModel
   openjij.model.model.make_BinaryQuadraticModel_from_JSON



Attributes
~~~~~~~~~~

.. autoapisummary::

   openjij.model.model.from_hising
   openjij.model.model.from_hubo
   openjij.model.model.from_ising
   openjij.model.model.from_numpy_matrix
   openjij.model.model.from_qubo
   openjij.model.model.from_qubo
   openjij.model.model.from_serializable
   openjij.model.model.from_serializable


.. py:data:: from_hising
   

   

.. py:data:: from_hubo
   

   

.. py:data:: from_ising
   

   

.. py:data:: from_numpy_matrix
   

   

.. py:data:: from_qubo
   

   

.. py:data:: from_qubo
   

   

.. py:data:: from_serializable
   

   

.. py:data:: from_serializable
   

   

.. py:function:: BinaryPolynomialModel(*args, **kwargs)


.. py:function:: BinaryQuadraticModel(linear, quadratic, *args, **kwargs)

   generate BinaryQuadraticModel object.

   .. attribute:: vartype

      variable type SPIN or BINARY

      :type: dimod.Vartype

   .. attribute:: linear

      represents linear term

      :type: dict

   .. attribute:: quadratic

      represents quadratic term

      :type: dict

   .. attribute:: offset

      represents constant energy term when convert to SPIN from BINARY

      :type: float

   .. attribute:: num_variables

      represents number of variables in the model

      :type: int

   .. attribute:: variables

      represents variables of the binary quadratic model

      :type: list

   :param linear: linear biases
   :type linear: dict
   :param quadratic: quadratic biases
   :type quadratic: dict
   :param offset: offset
   :type offset: float
   :param vartype: vartype ('SPIN' or 'BINARY')
   :type vartype: openjij.variable_type.Vartype
   :param gpu: if true, this can be used for gpu samplers.
   :type gpu: bool
   :param kwargs:

   :returns: generated BinaryQuadraticModel

   .. rubric:: Examples

   BinaryQuadraticModel can be initialized by specifing h and J::

       >>> h = {0: 1, 1: -2}
       >>> J = {(0, 1): -1, (1, 2): -3, (2, 3): 0.5}
       >>> bqm = oj.BinaryQuadraticModel(self.h, self.J)

   You can also use strings and tuples of integers (up to 4 elements) as indices::

       >>> h = {'a': 1, 'b': -2}
       >>> J = {('a', 'b'): -1, ('b', 'c'): -3, ('c', 'd'): 0.5}
       >>> bqm = oj.BinaryQuadraticModel(self.h, self.J)


.. py:function:: bqm_from_numpy_matrix(mat, variables: list = None, offset=0.0, vartype='BINARY', **kwargs)


.. py:function:: make_BinaryPolynomialModel(polynomial, index_type=None, tuple_size=0)


.. py:function:: make_BinaryPolynomialModel_from_JSON(obj)


.. py:function:: make_BinaryPolynomialModel_from_hising(*args, **kwargs)


.. py:function:: make_BinaryPolynomialModel_from_hubo(*args, **kwargs)


.. py:function:: make_BinaryQuadraticModel(linear: dict, quadratic: dict, sparse)

   BinaryQuadraticModel factory.

   :returns: generated BinaryQuadraticModel class


.. py:function:: make_BinaryQuadraticModel_from_JSON(obj: dict)

   make BinaryQuadraticModel from JSON.

   :returns: corresponding BinaryQuadraticModel type


