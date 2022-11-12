# 🔨 Hands-on: Staged deployments 

In this hands-on lab your will create environments and a staged deployment workflow with approvals.

This hands on lab is based on [My first workflow](05-My-first-workflow.md) and adds the following steps:
- [🔨 Hands-on: Staged deployments](#-hands-on-staged-deployments)
  - [Creating and protecting environments](#creating-and-protecting-environments)
  - [Point the deploy job to an environment](#point-the-deploy-job-to-an-environment)
  - [Reviewing and approving deployments](#reviewing-and-approving-deployments)

## Creating and protecting environments

1. Got to [Settings](/../../settings) | [Environments](/../../settings/environments) and click [New environment](/../../settings/environments/new)
2. Enter the name `Staging` and click `Configure environment`
3. Add yourself as the `Required reviewer` for this environment: 

<img width="349" alt="image" src="https://user-images.githubusercontent.com/5276337/174113475-967127de-45a7-4dc9-8477-4de4df62c7e6.png">

4. Only allow the `main`branch to be deployed to this environment:

<img width="350" alt="image" src="https://user-images.githubusercontent.com/5276337/174113782-70a1b18a-0ab9-49fd-a53e-cb2ea78916e1.png">

## Point the deploy job to an environment
1.  Open your build/deploy workflow file and find the `deploy` job
2.  In the depoloy job, add the yaml property `environment: staging`

```yaml
deploy:
    runs-on: ubuntu-latest
    needs: build
    environment: staging
```

## Reviewing and approving deployments

1. Open the workflow run and start the review.

<img width="600" alt="image" src="https://user-images.githubusercontent.com/5276337/174120029-f395e8ec-5e6e-4350-94c5-130caefaafc2.png">

2. And approve it with a comment:

![](/images/2022-11-12-14-29-40.png)

4. The result looks like this and contains the approval and the URL for the staging environment:

![](/images/2022-11-12-14-28-41.png)