# Contributing to terraform

1. [Getting Involved](#getting-involved)
2. [Questions and Discussion](#questions-and-discussion)
3. [Unit and Functional Tests](#unit-and-functional-tests)
4. [Versioning and Branching](#versioning-and-branching)


## Getting Involved

Contact with Cloud Enablement Team (CET) to give them a heads-up on what you want to contribute.

Understand the [Terraform Source Code Change Process](https://contegixapp1.livenation.com/confluence/display/AWS/Terraform+Souce+Code+Change+Process)

### A. Contribute to terraform source code

1. Start with terraform [README.md](https://github.com/hashicorp/terraform/blob/master/README.md)
   Get GO setup follow by README.md
   You need an account to get access github before you can contribute to terrform. 
   Contact with CET team to get access.

2. Set up current directory to $GOPATH/src/github.com/hashicorp

3. Clone https://github.com/ticketmaster/terraform master to $GOPATH/src/github.com/hashicorp:

     `git clone https://github.com/ticketmaster/terraform`

4. Next 3 steps are for rebasing github ticketmaster/terraform master branch to hashicorp/terraform master.

5. Setup upstream to github hashicorp/terraform master branch

     `git remote add upstream https://github.com/hashicorp/terraform.git`.

6. Rebase github ticketmaster/terraform with hashicorp/terraform's master

     `git fetch upstream`

     `git rebase upstream/master`

7. Push the updated master to github `git push`

8. If you only want to sync github ticketmaster/terraform with hashicorp ticketmaster/terraform, you can skip following steps

9. Create your feature branch :

     `git checkout -b my-new-feature`

10. Work on your code change, following with README.md and [Unit and Functional Tests](#unit-and-functional-tests) for test

11. Run `make` to compile the code and tests.

    Note: if `make` failed on other people's code, try `make dev`

12. Use `git squash` your multiple commits into one/small number of commits before submit pull request. That will make easy for us to do cherry-pick later.

    Reference [How to use git squash](https://ariejan.net/2011/07/05/git-squash-your-latests-commits-into-one/)

13. Push your changes to github branch  https://github.com/ticketmaster/terraform

      `git push --set-upstream origin my-new-feature`

14. Open a new pull request to hashicorp
    Provide details in pull request about your changes and communicate with Hashicorp. Make sure the buld is pass.

15. Once the PR is accepted, we need to refresh ticketmaster's gitlab terraform source code
    Put the accepted PR in [README-TM.md](http://git.tm.tmcs/AWS/terraform/blob/tm/README-TM.md) CherryPick list.



## Questions and Discussion

### Slack Channel
* \#aws


## Unit and Functional Tests
1. Modify or write the unit test code for terraform change. Test unit test by make

2. Functional test. Here is example to test build resource on ticketmaster's sandbox account (tm-sandbox)

 `declare -x AWS_PROFILE="tm-sandbox-Ops-Techops"`

 `declare -x AWS_REGION="us-east-1"`

 `make testacc TEST=./builtin/providers/aws TESTARGS='-run=<testname regexp>'`

3. If you want to use terraformer to test your changes, following with terraformer [CONTRIBUIING.md](http://git.tm.tmcs/AWS/terraformer/blob/master/CONTRIBUTING.md)


## Versioning and Branching
1. gitlab has no master branch. http://git.tm.tmcs/AWS/terraform tm branch is the latest code change

2. ticketmaster's github master branch is match to hashicorp master branch + ticketmaster's PR




