# Terraform Style Guide

## Terraform Automation SOP

1. Initialize the Terraform working directory.
2. Produce a plan for changing resources to match the current configuration.
3. Have a human operator review that plan, to ensure it is acceptable.
4. Apply the changes described by the plan.

Steps 1, 2 and 4 can be carried out using the familiar Terraform CLI commands, with some additional options:

`terraform init -input=false` to initialize the working directory.
`terraform plan -out=tfplan` -input=false to create a plan and save it to the local file tfplan.
`terraform apply -input=false` tfplan to apply the plan stored in the file tfplan.

The `-input=false` option indicates that Terraform should not attempt to prompt for input, and instead expect all necessary values to be provided by either configuration files or the command line. It may therefore be necessary to use the `-var` and `-var-file` options on terraform plan to specify any variable values that would traditionally have been manually-entered under interactive usage.

By default, some Terraform commands conclude by presenting a description of a possible next step to the user, often including a specific command to run next.

When the environment variable `TF_IN_AUTOMATION` is set to any non-empty value, Terraform makes some minor adjustments to its output to de-emphasize specific commands to run. The specific changes made will vary over time, but generally-speaking Terraform will consider this variable to indicate that there is some wrapping application that will help the user with the next step.

## Plugin Cache

When possible use a container that already contains the latest plugin releases from releases.hashicorp.com to ensure quicker build times and syncrounous deployment steps for higher enclave environments. The default directory for plugin pulls during the `terraform init` phase is .terraform in the working directory. The `plugin dir` can be set with the following command.

`terraform init -input=false -plugin-dir=/usr/lib/custom-terraform-plugins`
