# Cru App CloudRun Template
_Google CloudRun is currently in beta_

This is a template for a basic Cru Application using the Google ClourRun service. It includes the necessary configuration to build
and deploy the application to Google CloudRun using the [aws/cloudrun/app](https://github.com/CruGlobal/cru-terraform-modules/blob/main/aws/cloudrun/app/README.md) Terraform module.

## Bootstrap new Cru App
You can bootstrap a new GitHub repository and Cru Application using the [Add Cru Application](https://github.com/CruGlobal/cru-terraform/actions/workflows/cru-application.yml) GitHub workflow.
Click the `Run workflow` button and follow the prompts. This will create a Terraform Pull Request that when applied,
will create a new GitHub Repository using this template. Subsequent application environments (`production` or `staging`)
can be created using the [Add Cru App Environment](https://github.com/CruGlobal/cru-terraform/actions/workflows/cru-application-env.yml) GitHub workflow.

## Usage
The template application uses Ruby and Rails. You'll want to initialize a new rails application and commit the changes
to the repository. Alternatively, you can change to another language or framework. The Template assumes Rails out of
the box.

Builds and Deployments are managed by [build-deploy-cloudrun.yml](https://github.com/CruGlobal/cru-app-cloudrun-template/blob/main/.github/workflows/build-deploy-cloudrun.yml) GitHub workflow. The Build process executes the `build.sh` file which is responsible for
building a Docker container. After a successful build, the Deployment process triggers a deployment of the Application
in the [cru-deploy](https://github.com/CruGlobal/cru-deploy/actions/workflows/promote-cloudrun.yml) GitHub repository.
The build and deployment process will fail until the Terraform for the application environment has been applied. You can
comment out specific [branches](https://github.com/CruGlobal/cru-app-cloudrun-template/blob/main/.github/workflows/build-deploy-cloudrun.yml#L6-L8) to reduce the build failure noise until specific environments are ready.
Terraform is responsible for creating the permissions which GitHub uses to access the Google CloudRun service.
