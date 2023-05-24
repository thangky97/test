:py:mod:`openjij.sampler.chimera_gpu.base_gpu_chimera`
======================================================

.. py:module:: openjij.sampler.chimera_gpu.base_gpu_chimera


Module Contents
---------------

Classes
~~~~~~~

.. autoapisummary::

   openjij.sampler.chimera_gpu.base_gpu_chimera.BaseGPUChimeraSampler




.. py:class:: BaseGPUChimeraSampler

   Bases: :py:obj:`dimod.Structured`

   .. autoapi-inheritance-diagram:: openjij.sampler.chimera_gpu.base_gpu_chimera.BaseGPUChimeraSampler
      :parts: 1

   Abstract GPUChimera Sampler

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



