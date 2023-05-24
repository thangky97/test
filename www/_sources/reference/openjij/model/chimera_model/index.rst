:py:mod:`openjij.model.chimera_model`
=====================================

.. py:module:: openjij.model.chimera_model


Module Contents
---------------


Functions
~~~~~~~~~

.. autoapisummary::

   openjij.model.chimera_model.ChimeraModel
   openjij.model.chimera_model.make_ChimeraModel
   openjij.model.chimera_model.make_ChimeraModel_from_JSON



Attributes
~~~~~~~~~~

.. autoapisummary::

   openjij.model.chimera_model.from_ising
   openjij.model.chimera_model.from_qubo
   openjij.model.chimera_model.from_serializable


.. py:data:: from_ising
   

   

.. py:data:: from_qubo
   

   

.. py:data:: from_serializable
   

   

.. py:function:: ChimeraModel(linear: dict = None, quadratic: dict = None, offset: float = 0.0, vartype=SPIN, unit_num_L: int = None, model=None, gpu: bool = False)

   Generate ChimeraModel object

   This model deal with chimera graph.
   ChimeraModel provide methods to verify whether a given interaction graph
   matches a Chimera graph and to convert it to cxxjij.graph.Chimera.

   :param linear: linear biases
   :type linear: :class:`dict`
   :param quadratic: quadratic biases
   :type quadratic: :class:`dict`
   :param offset: offset
   :type offset: :class:`float`
   :param vartype: vartype ('SPIN' or 'BINARY')
   :param unit_num_L: unit_num_L
   :type unit_num_L: :class:`int`
   :param model: if model is not None, the object is initialized by model.
   :type model: :class:`BinaryQuadraticModel`
   :param gpu: if true, this can be used for gpu samplers.
   :type gpu: :class:`bool`

   :returns: generated ChimeraModel

   .. rubric:: Examples

   Example shows how to initialize ChimeraModel.::

       # This interactions satisfy chimera topology.
       >>> Q={(0, 4): -1, (4, 12): -1}
       >>> chimera_model = ChimeraModel(Q, unit_num_L=2)  # make
       >>> chimera_self.validate_chimera()


.. py:function:: make_ChimeraModel(linear, quadratic)

   ChimeraModel factory.

   :returns: generated ChimeraModel class


.. py:function:: make_ChimeraModel_from_JSON(obj)

   Make ChimeraModel from JSON.

   :returns: corresponding ChimeraModel type


