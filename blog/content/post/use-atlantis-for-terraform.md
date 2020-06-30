---
title: "Use Atlantis For Terraform"
date: 2020-06-30T17:49:21+02:00
archives: "2020"
author: goci.io
tags: [terraform, workflows, ci, tooling]
---

[Terraform](https://www.terraform.io/) can be used to automate the Provisiong of your Infrastructure. 
Usually Terraform will be used in Combination with a Remote State (for example an encrypted S3 Bucket) to store its last known State and create Diffs against.
It basically consits of the following three commands: `plan`, `apply` and `destroy`.

After changing some Terraform Code as next Step you want to be able to see the actual Difference you are creating by introducing your Change.
[Atlantis](https://www.runatlantis.io/) can be used to plan your Changes and automate your Pull- or Merge Requests.
Atlantis is deployed as Webhook Server waiting for new Events from a Version Control System (for example pushes or releases).

### Benefits 

There are sevaral advantages by using Atlantis:

1. Using Comments in your Pull Requests to Plan and Apply Changes
2. Workspace Definitions to clearly separate your Environments
3. Workflow Definitions to customize to your Needs and execute other Scripts
4. Restrictions on Repository-Level Configurations (Approvals, Workflows)
5. Debug failed Runs or Migrate State (Terraform CLI proxy)
6. No need for custom handwritten and error-prone scripts
7. Integrated Locking of Workspaces and Modules
8. Rollout Changes from a Branch and let Atlantis Auto-Merge the Branch upon Success
9. Simple UI to manage Locks and view open Change Requests

### Recommendations

After using Atlantis for a while here are some of our Recommendations on how to use it:

&nbsp;

#### 1. Take Time inspecting the Plan
Before you instruct Atlantis to execute your Plan, inspect and validate it properly. Once Atlantis starts applying your Changes the global State of Terraform changes and your Workspace will be locked. Failed Rollouts result in an invalid, current State and Rollouts from other Branches will "revert" your Changes and might even fail depending on the previously applied Changes.

#### 2. Branch Rollouts
Rolling out Changes from a Branch allows you to completely validate your Changes as Terraform can still fail during Apply even when a Plan was successfully created.
But we recommend to enable Auto-Merge of Branches upon successful Apply to reflect Changes to your State in the Version Control System.

#### 3. Enable Status Checks
We recommend to enable (if possible) a Status Check waiting for `"atlantis plan"` to ensure that no unplanned Changes are merged to the Master.
You can also configure Atlantis to reject Rollouts when there are any other Status Checks failing on the current Branch.

#### 4. Prevent Access to State Backend
Not only contains the Terraform State all of your Secrets but it is also required to make changes to your existing Resources and is pinned to a specific Terraform Version.
Prevent Humans from accessing the State Backend directly to avoid unintended Version-Upgrades and any Changes outside of your Version Control System.

#### 5. Configure Atlantis Server 
The Atlantis Server will be your primary Operator to execute Terraform and is also the "gate-keeper" for Changes to your Infrastructure. This includes Permissions from your CI System to apply Changes. Therefore we recommend to properly secure and setup your Atlantis Server, define Workflows and connect your Workflows to corresponding State Backends.

### Try it out

You can try it out now by using our [managed Atlantis-Offer](https://docs.goci.io/en/latest/providers/atlantis). On our managed Solution we will maintain the Atlantis Server itself including a trusted TLS Connection. [Sign up]() for goci.io to Get Started now just in a few Seconds. 

You can also deploy it yourself:
- Deploy to [AWS ECS](https://github.com/cloudposse/terraform-aws-ecs-atlantis)
- Deploy to Kubernetes [using Helm](https://github.com/goci-io/aws-atlantis-helm)
