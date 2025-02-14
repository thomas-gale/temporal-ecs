# AWS ECS - Temporal Deployment

A temporal deployment tool which lets you setup , deploy and get your temporal service running on ECS in few minutes. This tool deploys **Temporal Server** , **RDS** , **OpenSearch** and **Temporal UI**. **AWS Copilot** is used to do the deployment part.


# Getting Started 📌

- Pre - requisites :memo:
    - You need to have AWS Copilot setup in order to make the script work. If you haven't done it already, [go through this.](https://aws.github.io/copilot-cli/docs/getting-started/install/)
- Once you have all things in place , clone this repo and open it in any of your favourite IDE.
- Make sure you are in the root directory of the project, this is where you will execute the next steps.
- Run this command to give the execution permission to the script's.
  `chmod +x setup-temporal.sh update-temporal.sh`
- Run the script `./setup-temporal.sh envName permissionBoundary resourceTag`
- When prompted by copilot init
  `Would you like to deploy a test environment?`
    - Enter `N` (We will create our own env for deployment)
- Have a :popcorn: and watch the things being deployed :rocket:

## All about the script :magic_wand:

`./setup-temporal.sh` will take in three arguments and all are mandatory.

- **Env Name** - Specify the name for the environment which you want all the services to be deployed.
- **Permission Boundary** - Specify the policy to allow to create roles.
- **Resource Tag** - Specify the special tag that you want to apply to resources created by copilot.
# Setting up your temporal workflow.
Considering that you have some idea about temporal , let's see how you can use the deployed Temporal servers within your existing workflow and workers.
Incase you are new to temporal, you should consider going through [temporal first.](https://temporal.io/)

When the temporal server is deployed you will get a link on the terminal , you will need this link to point your workflow to the server.

Grab the link and pass it to your WorkflowServiceStubs -

    WorkflowServiceStubs service = WorkflowServiceStubs.newServiceStubs(  
        WorkflowServiceStubsOptions.newBuilder().setTarget("urlToTemporal:7233").build()  
        );
Also if you launch all the services in the same VPC (which is the case with the current deployment) you can simply use the `service discovery url's`  which will always be `{service_name}.{env_name}.{app_name}.local`.

You can read more about copilot service discovery [over here.](https://aws.github.io/copilot-cli/docs/developing/service-discovery/)

When the UI server is deployed you will get another link, this link will be used to see the dashboard for your workflow details.

# Update Script
`./update-temporal.sh` is all you need whenever you want to deploy any changes to the current ECS Infrastructure.
As AWS Copilot is being used under the hood, use this only if there are any changes; the script will deploy them or else it won't do any unnecessary deployment.

`./update-temporal.sh envName`

PS- Remember the basic's **Be in the root folder to run this script as well** :smile: