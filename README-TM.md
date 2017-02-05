1. [Introduction](#introduction)
2. [Outstanding PRs](#outstanding-pr)
3. [Rebase Terraform](#rebase-terraform)


# Introduction
This is Ticketmasters fork of Terraform that includes features we need that have not yet been merged into the upstream master.
This differs from master by:
Inclusion of this file, .gitlab-ci.yml, and CONTRIBUTING.md

# Repository Structure
The `tm` branch of this repository contains our commits that should be applied on top of a new release of Terraform. The best
way to do this is to rebase the commits from the `tm` branch onto a freshly checked out tagged release of upstream Terraform.

## Outstanding PRs

List of Outstanding PRs or commits, ordered by time:

Format: `<PR number> <commit hash>: <short description>`

For example:
* `8294` `95a86cc`: SNS Platform Application Support

### Included PRs
* `8294` `95a86cc`: SNS Platform Application Support

## Rebase Terraform
Here are the steps to build a new release of Terraform and include the Ticketmaster changes.

Hashicorp Terraform master branch is using tags for their official release version numbers. For example "v0.8.2"

1.  Terraform is stored on `https://git.tm.tmcs/AWS/terraform` with our changes in the `tm` branch. Clone the repository.


	```
	git clone git@git.tm.tmcs:AWS/terraform.git terraform-internal
	cd terraform-internal
	```

2. Pull down the official tag and update it with our changes

	```
	git remote add upstream https://github.com/hashicorp/terraform.git
	git fetch upstream
	git checkout refs/tags/v0.8.2 -b v0.8.2
	git rebase tm v0.8.2
	```

3. Include outstanding PRs

	Don't include any of the PRs that have been merged in. If they have been merged in remove them from the list in the `tm` branch.

 	We will use [8294](https://github.com/hashicorp/terraform/pull/8294) as an example.

	Add repository that you need to cherry pick from, in this case Ticketmasters.
	
	```
	git remote add tm-github https://github.com/ticketmaster/terraform.git
	git fetch tm-github
	```

	Now merge in the branch that the PR is from.

	```
	git rebase tm-github/SNS_PLATFORM_APPLICATION v0.8.2
	```

5. Push the changes to GitLab

	```
	git push origin refs/heads/v0.8.2
	```

6. Monitor the build for success.

7. Next step is to upgrade Terraformer. [CONTRIBUTING.md](http://git.tm.tmcs/AWS/terraformer/blob/master/CONTRIBUTING.md)

   Read the build output to get the version you will require for the terraformer build. For example `0.8.2_201609191958`. You will need it for terraformer build.

