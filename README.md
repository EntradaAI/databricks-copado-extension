# Databricks Copado Extension

## Setup & Customization Guide

### Introduction

The Databricks Copado extension extends the functionality of the Copado CI/CD platform in
order to work with Databricks Asset Bundles and Databricks Repos for a seamless deployment
process of Databricks pipelines. The extension leverages service principals in accordance with
Databricks deployment best practices and has a focus on automation, requiring very little
manual effort to set up. There is practically no limit on the customization of the pipeline as the
extension does not constrain the creation of the Databricks Asset Bundle for deployment at all,
rather, it just streamlines the deployment of the bundles.

### Setup

#### Prerequisites

1. Access to Copado
2. Access to Databricks
3. Workspaces for deployment setup with Unity Catalog
4. A service principal admin for each workspace needing deployment to, each with an
OAuth secret

5. A Databricks supported source control system with an account dedicated to deployment
and a token for each environment
6. Understanding and development of Databricks Asset Bundles

#### Setup

1. In your Copado workspace, create environments with credentials corresponding to your
Git branches (e.x. dev/test/prod). These should also match the DAB targets. There
should be a ‘localdev’ branch in Copado for deploying to the dev branch after completing
the User Story
2. In Copado, create hidden system properties (must be named exactly as below) for each
of these environments for:
    * DATABRICKS_CLIENT_SECRET (from step #4 of prerequisites)
    * GIT_TOKEN (from step #5 of prerequisites)

3. In your Copado pipeline, create environmental variables (connected to each
environment) for:
    * DATABRICKS_CLIENT_ID - The UUID of the service principal
    * GIT_USERNAME - The username of the Git account to which the Git tokens in the previous step are associated with (should be the same across environments)
4. Setup Git integration in Copado

### Customization

Feel free to add more parameters to the steps, particularly the deployment step. The base
extension does not come with built-in additional variables to DABs but they can be easily added
with script parameters.

### How to use it

Once everything is set up, simply create User Stories as usual. The User Story should be
created off of the dev branch. Once your local changes have been committed, deploy the User
Story down the line such as localdev -> dev and dev -> test. As deployment completes, observe
your Databricks workspace and the updated repos/workflows/pipelines that the deployment
process has automated.