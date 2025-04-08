# mobile-id-wallet-documentation
This repo contains documentation regarding our MobileID Wallet SDK for both Android and iOS with sample applications

# MobileID Wallet SDK Documentation

This repo will be used to store mkdocs project.

## Commands

- mkdocs build - Generate a folder "site" with the static content of the current markdown files and assets.
- mkdocs serve - Creates a local server that automatic renders the changes in markdown files to help in development mode.

Mike plugin offers the following commands to test, publish and manage versioning:

- mike list - Lists all the versions that are available in this project
- mike delete <version_name> - deletes the version name from the list of versions
- mike serve - starts localhost server
- mike deploy --push <version_name> - Deploys a new version from current branch with the name passed in the command
- mike deploy --push --update-aliases <version_name> latest - Deploys a new version and tags it as latest

Release that has the tag latest will be used automatically. 
Also when a user is viewing any other version that is not the latest, 
a banner will appear showing a warning that a new version is available.

### mkdocs
https://squidfunk.github.io/mkdocs-material/

### Mike cmd 
Install from official repo: https://github.com/jimporter/mike

## Deployment Process
Create a branch following this structure: "release/major.minor"

Prepare documentation and commit changes.

The github workflow "deploy-docs.yml" will create a pipeline to deploy the documentation automatically.

Mike will extract the major.minor version from the branch name and deploy it with that name.

**Warning** - Mike will always tag the version as latest, so if it's an hotfix it must be done manually.