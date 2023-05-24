:py:mod:`openjij.utils.graph_utils`
===================================

.. py:module:: openjij.utils.graph_utils


Module Contents
---------------


Functions
~~~~~~~~~

.. autoapisummary::

   openjij.utils.graph_utils.chimera_to_ind
   openjij.utils.graph_utils.qubo_to_ising



.. py:function:: chimera_to_ind(r: int, c: int, z: int, L: int)

   [summary]

   :param r: row index
   :type r: :class:`int`
   :param c: column index
   :type c: :class:`int`
   :param z: in-chimera index (must be from 0 to 7)
   :type z: :class:`int`
   :param L: height and width of  chimera-units (total number of spins is :math:`L \times L \times 8`)
   :type L: :class:`int`

   :raises ValueError: [description]

   :returns: corresponding Chimera index
   :rtype: int


.. py:function:: qubo_to_ising(mat: numpy.ndarray)

   Inplace-convert numpy matrix from qubo to ising.

   :param mat: numpy matrix
   :type mat: :class:`np.ndarray`


