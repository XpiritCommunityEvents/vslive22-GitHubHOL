# 🔨 Hands-on: GitHub Projects

In his hands-on lab you will practice working with GitHub projects. The exercise consists of the following parts:
- [🔨 Hands-on: GitHub Projects](#-hands-on-github-projects)
  - [Working with the backlog](#working-with-the-backlog)
  - [Working with boards](#working-with-boards)
  - [Workflows](#workflows)
  - [Fill the board](#fill-the-board)

## Working with the backlog

[:hammer_and_wrench: DIY Link](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/quickstart-for-projects)

1. Go to your GitHub profile | `Projects` and click `Create project`
2. Start with a normal table and give the project a name (i.e., `GitHub Bootcamp`)
3. In this repository, go to `Projects` and add the project you just created
4. Display the hidden `Labels`field
5. Add a new `Single Select` named `Level` with the values `Epic`, `Feature`, `Story`, and `Task`
6. Add a number field `Effort`
7. Add an iteration field `Sprint` with a two week cadence
8. Add an iteration field `Quarter` with a 12 week cadence
9. Add your existing issues with the correct levels and some other sample data
10. Group the backlog by level and safe the view.

<details><summary>Solution</summary>

  See [this example](https://github.com/users/<yourhandle>/projects/9)
  
</details>

## Working with boards

[:hammer_and_wrench: DIY Link](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/quickstart-for-projects#adding-a-board-layout)

1. Create a Kanban Board filtered by `level:Feature` and safe it as `Feature Board`
2. Create a Kanban Board filtered by `level:story` and change the column field to sprint. Safe the view as `Sprints`
3. Create a Kanban Board filtered by `-level:story` and change the colun view to `Quarter`. Safe the view as `Planning`.

<details><summary>Solution</summary>

  - [Feature Board](https://github.com/users/<yourhandle>/projects/9/views/2)  
  - [Sprints](https://github.com/users/<yourhandle>/projects/9/views/2)  
  - [Planning](https://github.com/users/<yourhandle>/projects/9/views/5)  
  
</details>

## Workflows
[:hammer_and_wrench: DIY Link](https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/using-the-built-in-automations)

1. Enable all the default workflows
2. Transition some issues and see how the status changes.

## Fill the board

* Create 1 Epics / Features / Stories 
  * [Epic] Authentication & Authorization
    * [Feature] Login Page
      * [Story] As a user I can access the  Login Page
      * [Story] As a user I can login with Facebook
      * [Story] As a user I can login with Google
    * [Feature] Implement GDPR Rights
      * [Story] As a user I can remove my account
      * [Story] As a user I can request all my data
      * [Story] As a user I cann fill in a form to fulfill my GDPR rights
  * Create these 3 Bugs
    * [Bug] Discount amount shows the wrong amount -> $100 
    * [Bug] :beetle: Highly Recommended section should be without exclamation mark ! 
    * [Bug] Fix Login Button
     

* Create 3 sprints in the board by using Iterations
* Setup a sprint backlog by dragging items in the sprint




