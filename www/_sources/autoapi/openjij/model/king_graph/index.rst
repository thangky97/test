:py:mod:`openjij.model.king_graph`
==================================

.. py:module:: openjij.model.king_graph


Module Contents
---------------


Functions
~~~~~~~~~

.. autoapisummary::

   openjij.model.king_graph.KingGraph
   openjij.model.king_graph.make_KingGraph
   openjij.model.king_graph.make_KingGraph_from_JSON



Attributes
~~~~~~~~~~

.. autoapisummary::

   openjij.model.king_graph.from_ising
   openjij.model.king_graph.from_qubo
   openjij.model.king_graph.from_serializable


.. py:data:: from_ising
   

   

.. py:data:: from_qubo
   

   

.. py:data:: from_serializable
   

   

.. py:function:: KingGraph(linear=None, quadratic=None, offset=0.0, king_graph=None, vartype=SPIN, machine_type='')

   generate KingGraph model.

   :param linear: linear biases
   :type linear: dict
   :param quadratic: quadratic biases
   :type quadratic: dict
   :param offset: offset
   :type offset: float
   :param king_graph: represents ising or QUBO interaction.
                      Each spins are decided by 2-d corrdinate x, y.

                      * Quadratic term: [x1, y1, x2, y2, value]
                      * Linear term:    [x1, y1, x1, y1, value]
   :param vartype: 'SPIN' or 'BINARY'
   :param machine_type: choose 'ASIC' or 'FPGA'
   :type machine_type: str

   :returns: generated KingGraphModel

   .. rubric:: Examples

   The following code shows intialization of KingGraph::

       >>> h = {}
       >>> J = {(0, 1): -1.0, (1, 2): -3.0}
       >>> king_graph = oj.KingGraph(machine_type="ASIC", linear=h, quadratic=J)

   You can initialize it from `king_interaction`::

       >>> king_interaction = [[0, 0, 1, 0, -1.0], [1, 0, 2, 0, -3.0]]
       >>> king_graph = oj.KingGraph(machine_type="ASIC", king_graph=king_interaction)


.. py:function:: make_KingGraph(linear=None, quadratic=None, king_graph=None)

   KingGraph factory
   :returns: generated KingGraph class


.. py:function:: make_KingGraph_from_JSON(obj)

   KingGraph factory for JSON
   :param obj: JSON object
   :type obj: dict

   :returns: generated KingGraph class


