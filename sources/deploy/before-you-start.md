main_section: Deploy
sub_section: Overview

# before-you-start



##Configuration

Your pipelines are defined through yml-based configuration files. The [shippable.yml](/platform/tutorial/workflow/shippable-yml/) file contains definitions of the jobs, resources, and triggers in your pipeline.

Pipeline configuration files should be committed to a repository in your source control. This repository is called a [sync repository](#sync). You can keep these config files with the source code for your application or keep it separate in its own repository.

<a name="sync"></a>
##Sync repository

A source control repository that contains your pipeline configuration files is called a **Sync Repository**. Each sync repository contains `shippable.yml` files.

You must seed your pipeline with at least one sync repository through the Shippable UI. Subsequent sync repositories can also be added through the UI following the same process. Instructions are in the [Adding a sync repository](#seedPipeline) section below.

You may have the entire pipeline configuration maintained in one repository, split it across directories within the same repository, or split up the configuration across multiple sync repositories. This decision depends on your organizational preferences, as well as [security and permissions requirements](#permissions). For example, you may have pipeline configuration for source control through your first test environment in one repo, configuration for subsequent test environments in another repo, and configuration for your production environment in yet another repo. In this way, you can manage who can configure and execute different areas of your pipeline based on the permissions set on each repo.


<a name="seedPipeline"></a>
###Adding a sync repository

You can add a sync repository by following the steps below:

* First, add a subscription integration for the source control provider where your sync repository is located. Instructions are here - [Source Control Provider Integrations](/platform/integration/overview#source-control-providers).
* Go to your Organization's page on Shippable. A list of all available Organizations can be accessed by clicking on the Subscriptions menu at the top left of your screen:

<img width="30%" height="30%" src="/images/platform/integrations/list-subscriptions.png" alt="List of subscriptions">

* Click on the **Pipelines** tab
* If you have never added a sync repository, your Single Pane of Glass will be empty. Click the **+** button at upper right to add a sync repository.
* Complete the **Add Resource** fields:
	* The subscription integration dropdown should show the integration you created in the first step. If not, you will need to go through the flow of adding the integration.
	* The **Select Project** dropdown will show all repositories in the source control you just connected with the integration. Choose your sync repository.
	* Select the branch of the sync repository that contains your pipeline configuration files.
	* Name your sync repository with an easy to remember name.
* Click on **Save** to apply your sync repository configuration.

At this point, Shippable will parse all configuration files in the sync repository and create your pipeline(s). You will see a visualization of the the jobs and resources from your configuration files in the Single Pane of Glass (SPOG).

###Troubleshooting pipeline errors

If your rSync job fails or you do not see what you expected, you likely have a configuration error. Click on the rSync job in the SPOG view to see the console. Expand the **Executing Managed Task: rSync** section and then the **/home/shippable/micro/nod/stepExec/managed/rSync/run.sh** sections. This is the section that shows the console for your configuration. Configuration errors are shown highlighted in red at the end of this section as shown below.

<img src="/images/getting-started/rsync-errors.png" alt="Errors during pipelines config import"">

<a name="permissions"></a>
## Permissions

Permissions for your deployment pipelines are tightly coupled with permissions for your sync repositories. Consequently, pipeline elements are only visible and accessible to perform actions to users with **Owner**, **Collaborator/Write**, or **Read** access to the sync repository that holds the configuration files. Users that do not have access to your sync repository will not have access to that portion of your pipeline, even if they are members of your organization.
