**************************
Custom Resource Definition
**************************

Tools at goci.io are defined using a `Custom Resource Definition <https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/>`_
They simplify and group required Configuration for Applications and Services. Our System observes changes to any Tool in our System.
To fulfill the desired State our Watcher creates Jobs to provision, modify or destroy your Tool.

Manifest
--------

Below you can find the full Resource Definition. You can also suggest changes to it on `GitHub <https://github.com/goci-io/goci-community/edit/master/_static/assets/crds/tool.yaml>`_ 

.. literalinclude:: /_static/assets/crds/tool.yaml
   :language: yaml

As goci.io only offers a small Set of Tools initially we have decided to use a single `Tool` Resources.
This might change in the future. 
