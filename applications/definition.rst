**************************
Custom Resource Definition
**************************

Applications at goci.io are defined using a `Custom Resource Definition <https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/>`_
They simplify and group required Configuration for Applications and Services. Our System observes changes to any Application in our System.
To fulfill the desired State of your Application our Watcher creates a new Kubernetes Job to provision your Setup.

Manifest
--------

Below you can find the full Resource Definition. You can also suggest changes to it on `GitHub <https://github.com/goci-io/goci-community/edit/master/_static/assets/crds/application.yaml>`_ 

.. literalinclude:: /_static/assets/crds/application.yaml
   :language: yaml
