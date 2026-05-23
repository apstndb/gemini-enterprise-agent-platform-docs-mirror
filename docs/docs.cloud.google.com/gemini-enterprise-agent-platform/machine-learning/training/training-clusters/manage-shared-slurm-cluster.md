---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-shared-slurm-cluster
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-shared-slurm-cluster
title: 'Tutorial: Manage accounts and job scheduling on a cluster'
description: Optimize shared Slurm cluster resource allocation. Configure accounts, QOS, and preemption to enforce limits and prioritize jobs across teams.
data_source: docs.cloud.google.com
---

If you're interested in Gemini Enterprise Agent Platform training clusters, contact your sales representative for access.

This guide demonstrates how to use Slurm's accounting and [Quality of Service (QOS)](https://slurm.schedmd.com/qos.html) features to effectively manage a single training cluster shared by multiple teams with different priorities and resource needs.

## The Goal

By the end of this tutorial, you'll have a framework for managing cluster resources that can:

  - Enforce resource limits per team.
  - Prioritize and preempt jobs based on urgency.
  - Provide clear accounting for resource consumption.
  - Maximize cluster utilization while maintaining fairness.

## Prerequisites

  - A running training cluster with Accounting, Preemption and Priority configured to manage accounts, schedule and prioritize jobs.

  - [Orchestrate](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/orchestration)

  - [Advanced Slurm settings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#advanced-slurm-settings)

  - `sudo` access on the cluster's login node to run administrator commands.

## Core concepts: The building blocks of Slurm accounting

Slurm uses a clear and flexible hierarchy to manage resources. Understanding these four building blocks is key.

| Component     | Example                  | Purpose                                                                                                                      |
| :------------ | :----------------------- | :--------------------------------------------------------------------------------------------------------------------------- |
| **Account**   | A team or project        | The primary unit for grouping users and setting overall resource limits (for example, `team_ace` can use a max of 10 nodes). |
| **User**      | An individual researcher | The person submitting a job. Every user must belong to a default account.                                                    |
| **Partition** | A hardware queue         | A logical grouping of nodes. For maximum flexibility, we recommend a single partition containing all your nodes.             |
| **QOS**       | A rulebook               | A named set of rules that defines job limits (for example, "jobs in this QOS can only use 2 nodes") and scheduling priority. |

With this model, you can set a high-level quota for an entire account and apply a more granular, *per-job* limit using a QOS.

## The personas: Admin versus researcher

Two distinct roles interact with this system: the cluster administrator and the researcher.

### Cluster administrator

  - Primary tool: `sacctmgr` (Slurm account manager)
  - Your job: You build the "scaffolding" of accounts, users, and QOS rules. This is typically a "configure-once, update-as-needed" task.
  - Key tasks: Create accounts, assign users to accounts, define QOS rulebooks, and link them together.

### Researcher

  - Primary tools: `sbatch` , `squeue` , `sinfo`
  - Their job: Submit and monitor their research jobs.
  - The magic: When a researcher submits a job, Slurm automatically checks the rules associated with their account and QOS. If the job violates any limit, Slurm rejects it with a clear error message.

## The tutorial: A progressive walkthrough

The following tutorial puts these concepts into practice through a series of progressive scenarios. For this walkthrough, assume the role of the cluster administrator. Your task is to set up one account, `team_ace` , and one user, `user_alice` . The scenarios begin with no limits and progressively add layers of control.

### Part 1: Initial setup (no limits)

Create the account and associate the user.

  - The goal: Create the basic hierarchy for `team_ace` and `user_alice` .
  - The method: Use `sacctmgr` to add an account and then add a user associated with that account.

<!-- end list -->

    # --- (Run as Admin) ---
    
    # 1. Create the 'team_ace' account
    sudo sacctmgr add account team_ace Description="The Ace Team"
    
    # 2. Create the 'user_alice' user and map them to their default account
    # (Note: 'user_alice' must already exist as a Linux user on the node)
    sudo sacctmgr add user user_alice Account=team_ace
    
    # 3. Show the hierarchy we just built to confirm
    sacctmgr show associations where account=team_ace

Result: As the user `user_alice` , you can now submit a large job. Since no limits exist, a 7-node job is accepted and runs immediately (assuming 7 nodes are idle).

### Part 2: Add group-level limits to an account

Next, apply a resource cap to the `team_ace` account, limiting the entire team to a maximum of 6 nodes and 4 total jobs.

  - The goal: Set a total resource cap for an entire team.

  - The method: We apply this limit to the `team_ace` account using [`GrpJobs`](https://slurm.schedmd.com/resource_limits.html#assoc_grpjobs) (Group Jobs) and [`GrpTRES`](https://slurm.schedmd.com/resource_limits.html#assoc_grptres) (Group Trackable Resources, in this case, `node=6` ).

<!-- end list -->

    # --- (Run as Admin) ---
    
    # 1. Add group-level job and node limits to the 'team_ace' account
    sudo sacctmgr modify account where name=team_ace set GrpJobs=4 GrpTRES=node=6
    
    # 2. View the limits to confirm the change
    sacctmgr show association where account=team_ace

Results: To verify the new limits are working, perform the following tests as `user_alice` :

1.  Node limit: Submitting a 7-node job now fails. The job is put in a pending ( `PD` ) state with the reason ( `AssocGrpNodeLimit` ).
2.  Job limit: Submitting 5 single-node jobs results in 4 jobs running ( `R` ) and the 5th job pending ( `PD` ) with the reason ( `AssocGrpJobsLimit` ).

The account-level limits are working perfectly.

### Part 3: Add a per-job limit with QOS

The account-level group limit is effective for capping a team's total resource usage. However, it doesn't prevent a user from submitting a single job that consumes the entire team's quota. To control the size of *individual* jobs, the next step is to use a [Quality of Service](https://slurm.schedmd.com/qos.html) (QOS).

  - The goal: Restrict the maximum size of any individual job submitted by the team.
  - The method: We will create a Quality of Service (QOS) named `qos1` with a `MaxTRESPerJob=node=2` rule. We will then make this the default QOS for the entire `team_ace` account.

<!-- end list -->

    # --- (Run as Admin) ---
    
    # 1. Create a QOS with a per-job limit of 2 nodes
    sudo sacctmgr add qos qos1 MaxTRESPerJob=node=2
    
    # 2. Allow the 'team_ace' account to use this QOS
    sudo sacctmgr modify account where account=team_ace set QOS=qos1
    
    # 3. Set 'qos1' as the DEFAULT QOS for all users in this account
    sudo sacctmgr modify account where account=team_ace set DefaultQOS=qos1

Result: Now, if `user_alice` submits a 3-node job, the job is placed into a pending state with the reason ( `QOSMaxNodePerJobLimit` ). The user is still within their total *account quota* (6 nodes), but they have violated the per-job *QOS* rule.

### Part 4: Add a user-specific override

What if `user_alice` is an intern and needs to be restricted to even smaller jobs, without affecting the rest of the team?

  - The goal: Apply a more restrictive limit to a single user.
  - The method: We'll create a new, more restrictive QOS ( `qos_intern` ) and apply it as the default specifically for `user_alice` . This overrides the account's default QOS.

<!-- end list -->

    # --- (Run as Admin) ---
    
    # 1. Create a more restrictive QOS with a 1-node limit
    sudo sacctmgr add qos qos_intern MaxTRESPerJob=node=1
    
    # 2. Allow the account to use this new QOS
    sudo sacctmgr modify account where account=team_ace set QOS+=qos_intern
    
    # 3. Apply 'qos_intern' as the default QOS for the specific user association
    sudo sacctmgr modify user where name=user_alice account=team_ace set DefaultQOS=qos_intern

Result: If `user_alice` tries to submit the 2-node job that was previously allowed under `qos1` , it fails with ( `QOSMaxNodePerJobLimit` ). The more specific user-level rule has successfully overridden the general account-level rule.

### Part 5: Configure priority and preemption

Finally, configure job [priority and preemption](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/orchestration#preemption-priority) to ensure critical jobs can run immediately, even if the cluster is full.

  - The goal: Create a high-priority "urgent" QOS that can pause or cancel a lower-priority job to free up resources.

  - The method:
    
    1.  Create a new `qos_urgent` with a high `Priority` value.
    2.  Tell `qos_urgent` that it's allowed to `Preempt` jobs running in `qos1` .
    3.  Configure `qos1` to `REQUEUE` its jobs when they're preempted.

<!-- end list -->

    # --- (Run as Admin) ---
    
    # 1. Create a new 'qos_urgent' with a high priority that can preempt 'qos1'
    sudo sacctmgr add qos qos_urgent Priority=1000 Preempt=qos1
    
    # 2. Configure 'qos1' to requeue preempted jobs after a 10-second grace period
    sudo sacctmgr modify qos where name=qos1 set PreemptMode=REQUEUE GraceTime=10
    
    # 3. Allow the 'team_ace' account and 'user_alice' to use this new QOS
    sudo sacctmgr modify account where account=team_ace set QOS+=qos_urgent
    sudo sacctmgr modify user where name=user_alice account=team_ace set QOS+=qos_urgent
    
    # 4. For this scenario, remove the group limits so preemption is easier to trigger
    sudo sacctmgr modify account where name=team_ace set GrpJobs=-1 GrpTRES=node=-1

Result:

1.  In one terminal, `user_alice` submits a long-running job with the default `qos1` . It starts running ( `R` ).
2.  In a second terminal, `user_alice` submits a large job using the urgent QOS ( `sbatch --qos=qos_urgent ...` ).
3.  Within seconds, the first job's state changes from running (R) to pending ( `PD` ) with a reason of ( `Preempted` ). The urgent job then starts running.

Success\! You have configured a system where high-priority work automatically displaces low-priority work.

## Summary and next steps

By following this tutorial, you've learned to use Slurm's hierarchical accounting features to achieve granular control over a shared cluster. You can now:

  - Set global limits: Use accounts to set total resource quotas for entire teams.
  - Enforce per-job rules: Use QOS to control the size and priority of individual jobs.
  - Create specific overrides: Apply a different QOS to a User for fine-grained control.
  - Guarantee priority: Configure preemption to ensure critical workloads can always run.

This layered model provides a flexible and powerful way to manage cluster resources fairly and efficiently. For even more advanced configurations, refer to the [official Slurm documentation](https://slurm.schedmd.com/documentation.html) .
