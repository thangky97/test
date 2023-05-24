:py:mod:`openjij.model`
=======================

.. py:module:: openjij.model


Submodules
----------
.. toctree::
   :titlesonly:
   :maxdepth: 1

   chimera_model/index.rst
   king_graph/index.rst
   model/index.rst


Package Contents
----------------


Functions
~~~~~~~~~

.. autoapisummary::

   openjij.model.BinaryPolynomialModel
   openjij.model.BinaryQuadraticModel
   openjij.model.bqm_from_numpy_matrix
   openjij.model.make_BinaryPolynomialModel
   openjij.model.make_BinaryPolynomialModel_from_JSON
   openjij.model.make_BinaryPolynomialModel_from_hising
   openjij.model.make_BinaryPolynomialModel_from_hubo
   openjij.model.make_BinaryQuadraticModel



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


