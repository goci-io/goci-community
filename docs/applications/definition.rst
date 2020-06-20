**************************
Custom Resource Definition
**************************

Applications at goci.io are defined using a `Custom Resource Definition <https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/>`_
They simplify and group required Configuration for Applications and Services. Our System observes changes to any Application in our System.
To fulfill the desired State of your Application our Watcher creates a new Kubernetes Job to provision your Setup.

Manifest
--------

You can find the complete Resource Definition `here </_static/assets/crds/application.yaml>`_
