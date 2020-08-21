*******************************************
Install Managed Atlantis for AWS on goci.io
*******************************************

`Atlantis <https://www.runatlantis.io/>`_ can be used to automate your Terraform Workflows by using Comments in Change Requests.
You can download and use any Terraform Version you want, migrate State, adding Requirements to terraform apply Runs, run Jobs in Parallel and much more.

In this Article We will explain what's necessary to Setup and Run Atlantis. 
We also show how to install a managed Atlantis-Server on goci.io in just a few Minutes.

Terraform State Backend
#######################

To calculate Terraform Plans, Atlantis needs Access to your State File. State Files should be stored on a reliable and encrypted Storage System as it contains the last known Terraform State, Resource References and all Secrets used in your Code. 
We also recommend to enable Versioning for your State Files. Achieving this is easy by using an `AWS S3 Bucket <https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingBucket.html>`_ for Terraforms `State Backend <https://www.terraform.io/docs/backends/types/s3.html>`_.  
Using S3 as Terraform Backend also comes with the Ability to use a `DynamoDB Table <https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/WorkingWithTables.html>`_ to enable Locking, preventing multiple Applys on the same State. 
Even Atlantis comes with its own Locking on a per-Change-Request Basis we still recommend to use Terraforms Locking Feature to avoid collisions with other Apply-Runs (eg. another Branch or Human from their Local Environment).

Generelly we recommend to **not** grant any Humans (Read-)Write-Access to your Terraform State Backend. 
Make all your Changes using Atlantis Comments in your Change Requests. 
If you are working in a Team we also recommend to only allow Atlantis to Apply any Plans once someone else reviewed and approved the Plan.

Deploying Atlantis Server
#########################

Deploying the Atlantis-Server can be achieved by using the `Helm Chart <https://github.com/helm/charts/tree/master/stable/atlantis>`_. 
Goci has already a preconfigured Terraform Module to spin up a new Atlantis-Server including all required Resources like an AWS S3 State Backend, IAM Role and a Webhook Secret.

`github.com/goci-io/aws-atlantis-helm <https://github.com/goci-io/aws-atlantis-helm/>`_ 

**Cold Start**: In case you do not have a separate Terraform Pipeline and State Backend to provision Atlantis Resources you will need to make sure you do not loose Access to the State File.
Using goci.io's managed Atlantis Server enables you to start with Atlantis and Terraform right from the Beginning.
You wont need to worry about the initial Setup and State of your Atlantis Installation.
