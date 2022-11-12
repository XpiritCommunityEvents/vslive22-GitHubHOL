# 🔨 Hands-on: Adding automated build & 4 eyes principle to your repository

## Objectives of this hands-on lab
This hands-on lab you will learn how to add compliancy to your GitHub repository. github takes for everything a Developer first approach and has a number of capabillities that help you enforce compliancy. In this lab we will help you set up the following concepts related to compliance:

This hands-on lab consists of the following steps:
- [🔨 Hands-on: Adding automated build & 4 eyes principle to your repository](#-hands-on-adding-automated-build--4-eyes-principle-to-your-repository)
  - [Objectives of this hands-on lab](#objectives-of-this-hands-on-lab)
    - [Create a Branch Protection Rule](#create-a-branch-protection-rule)
      - [Verify](#verify)
    - [Create a CI build for every Pull Request](#create-a-ci-build-for-every-pull-request)
    - [Use the CI build as a branch protection](#use-the-ci-build-as-a-branch-protection)
    - [Enforce CODEOWNERS review](#enforce-codeowners-review)
  - [Add Test Result Reports](#add-test-result-reports)

### Create a Branch Protection Rule
We want to protect our branches against unwanted direct updates. This is a very common setup in the enterprise.
In this exercise we will create a branch rule that prevents you to commit to the main branch directly and require you to create a pull request.

In your GitHub repo go to the settings tab and click the branches option as shown here:

![](/images/2022-11-12-13-45-58.png)

Now add a new rule and define which branch you want to protect. e.g. provide the pattern name `main`
Next you select the following options:
1. `Require a pull request before merging`
2. `Do not allow bypassing the above settings`


Now save this Branch Rule and see if it works.

#### Verify
To check if it works, create a change on one of the files that is in the main branch. Just use the portal to make the change and verify that the moment you want to commit the change you see the below indicator that you need to create a new branch before you can commit

Now, create a new branch and create a pull request that enables the code review from someone else in your organization/repository.


### Create a CI build for every Pull Request
In the previous module you created a workflow that builds and deploys the web application. This working workflow does everything from building to uploading the artefact. We have seen that the `Publish` step is somewhat slow and we are uploading artifacts on each run. Since you pay for the storage space for each artifact as well as for the action minutes, we can create a workflow that only does this when needed: after a Pull Request has completed.

1. Create a new workflow and only add the steps up until the `Test` step. This is enough to run the CI build, is fast and thus can be used for a fast pull request check. Since we don't need to the deploy the results of the pull request, we can save a lot of storage space.
1. The new workflow needs to be only triggered on a Pull Request. Tip :bulb: : Check the `on:` triggers  
1. Update the previous workflow to only run on changes on the `main` branch and not on a Pull Request.

### Use the CI build as a branch protection

In your GitHub repo go to the settings tab and click the branches option as shown here:

![branch protection rules](../images/branch-protection-rules.png)

Now modify the rule.

1. Add a branch protection rule to add the new PR workflow as a check on the Pull Request before it can be merged. For this use the `Require status checks to pass before merging` rule and select the job CI.
4. Make a code change on a new branch and observe what happens.

### Enforce CODEOWNERS review

If you want to enforce certain teams can only approve parts of the codebase, like a web development team for all the web application code and a docs team for the documentation, you can use the code owners file. We can enforce the code owners need to be part of the review process by adding this to the Branch Protection Rule.
There is already a CODEOWNERS file in the repo that you migrated. It has the following contents:

```
# Example, any change in this repo 
# will require approval from @vriesmarcel
# * @vriesmarcel

# Any change inside the `/Documents` directory
# will require approval from anyone in the organization fluentbytes and the team docsteam
# The team will need explicit write permissions to the repo for this to work!
# /Documents @fluentbytes/docsteam
# Create your own rules below this line without the # sign
```
Now change the file so it defines the folder `/TailwindTraders.Website/Source/Tailwind.Traders.Web` has a team as owner. All attendees of todays technical workshop are part of a team that we set up. this team has the following name: `vslive-orlando2022`.

The Team has access to your repository.

After setting up the file, commit it to the main branch (use a Pull Request!). Next go to the branch protection rules and for the main branch select the option `Require review from Code Owners`

Save the branch protection rule and make a change to e.g. the startup.cs file and see if you can commit the changes to the main branch. Ask one of the other attendees to review the pull request you created and see if it then is allowed to approve and merge the pull request. Please use the teams chat to find a colleague who can approve your pull request. If you can't find anyone, ask the instructors. 





