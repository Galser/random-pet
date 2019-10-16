# random-pet
Skills map - 200 Terraform, remote state

Follow-up repo for the skills map

# Main code

We prepare in this repo the code and then run state, to reference it in the next Lab task
- Code in [main.tf](main.tf)
  ```terraform
  terraform {
    backend "atlas" {
      name    = "galser-paid/random-pet"
    }
  }

  resource "random_pet" "demo" { }

  output "demo" {
    value = "${random_pet.demo.id}"
  }
  ```
- Init :
  ```
  terraform init 

  Initializing the backend...

  Successfully configured the backend "atlas"! Terraform will automatically
  use this backend unless the backend configuration changes.

  Initializing provider plugins...

  The following providers do not have any version constraints in configuration,
  so the latest version was installed.

  To prevent automatic upgrades to new major versions that may contain breaking
  changes, it is recommended to add version = "..." constraints to the
  corresponding provider blocks in configuration, with the constraint strings
  suggested below.

  * provider.random: version = "~> 2.2"

  Terraform has been successfully initialized!

  ```
- Run :
  ```
  terraform apply

  An execution plan has been generated and is shown below.
  Resource actions are indicated with the following symbols:
    + create

  Terraform will perform the following actions:

    # random_pet.demo will be created
    + resource "random_pet" "demo" {
        + id        = (known after apply)
        + length    = 2
        + separator = "-"
      }

  Plan: 1 to add, 0 to change, 0 to destroy.

  Do you want to perform these actions?
    Terraform will perform the actions described above.
    Only 'yes' will be accepted to approve.

    Enter a value: yes

  random_pet.demo: Creating...
  random_pet.demo: Creation complete after 0s [id=dashing-loon]

  Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

  Outputs:

  demo = dashing-loon
  ```
- Let's check remote state in TFE : 
state : `New state #sv-cav2oTqvoFd2hqpN`
  ```json
  {
    "version": 4,
    "terraform_version": "0.12.9",
    "serial": 0,
    "lineage": "6f70e2c6-cf02-6d74-d972-d4613c63636b",
    "outputs": {
      "demo": {
        "value": "dashing-loon",
        "type": "string"
      }
    },
    "resources": [
      {
        "mode": "managed",
        "type": "random_pet",
        "name": "demo",
  ```
  We've done here
