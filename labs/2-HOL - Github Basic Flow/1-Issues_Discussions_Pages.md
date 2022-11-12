# 🔨 Hands-on: Collaboration using Issues, Discussions, and Pages

In this hands-on lab you will practice to work with GitHub Issues, Discussions, and Pages. You will practice working with markdown, learn about issue templates and rendering markdown as a web page. The lab consists of the following parts:

- [🔨 Hands-on: Collaboration using Issues, Discussions, and Pages](#-hands-on-collaboration-using-issues-discussions-and-pages)
  - [Working with Issues and Templates](#working-with-issues-and-templates)
    - [Create an Issue](#create-an-issue)
    - [Nesting issues](#nesting-issues)
    - [Enabling discussions](#enabling-discussions)
    - [Issue templates](#issue-templates)
      - [Epic Template](#epic-template)
      - [Bug Template](#bug-template)
    - [Creating a Custom Form](#creating-a-custom-form)
  - [Participating in Discussions](#participating-in-discussions)
  - [Rendering markdown as HTML with GitHub Pages](#rendering-markdown-as-html-with-github-pages)

## Working with Issues and Templates

### Create an Issue
Create an Issue and add [markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) elements.

[:hammer_and_wrench: DIY Link](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

1. Add headers
1. Add lists and task lists
1. Add images and video
1. Use emojis   
1. Mention a person or team (using <kbd>@</kbd>)
1. Add a syntax-highlighted code block
1. Add a flow chart and try [different variants](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams)



### Nesting issues

[:hammer_and_wrench: DIY Link](https://docs.github.com/en/actions/managing-issues-and-pull-requests/adding-labels-to-issues)
1. Create and apply a label `Epic` to the issue
1. Add three tasks to the issue and convert them to issues
1. Create a label `Feature`and mark the 3 issues with this label
1. Add two tasks to each feature and convert them to issues 
1. Mark them with the label `Story` (create a label first)(use bulk edit!)


### Enabling discussions 

[:hammer_and_wrench: DIY Link](https://docs.github.com/en/discussions/quickstart)

Discussions are a great way to have a conversation in your team or with your users. In order to use discussions you need to enable discussions in your settings page.

* In your repository go to Settings
* In the General tab, scroll to features and enable discussions

### Issue templates

#### Epic Template
[:hammer_and_wrench: DIY Link](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository)

1. Create an issue template for an Epic
2. Create a config.yml file in the `.github/ISSUE_TEMPLATE`folder   
3. In the config.yml file, disable blank issues
4. Add an additional URL that points to a new discussion  

    <details><summary>Solution</summary>

    ```yaml
    blank_issues_enabled: false
    contact_links:
      - name: 👥 Discussions
        url:  https://github.com/<yourhandle>/<yourproject>/discussions/new
        about: Please use discussions for issues that are not a bug, enhancement or feature request
    ```

    </details>

#### Bug Template
[:hammer_and_wrench: DIY Link](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository)

1. Add a template for a bug report (`.github/ISSUE_TEMPLATE/bug_report.md`)
1. Assign bugs to yourself and add labels `bug` and `unplanned` to bugs
1. Prefix the title with `[Bug]:` and add some sample markdown.

    <details><summary>Solution</summary>    

    ```yaml
    ---
    name: 🐞 Bug report
    about: Create a report to help us improve
    title: '[Bug]:'
    labels: [bug, unplanned]
    assignees: 
      - <yourhandle>
    ---

    **Describe the bug**
    A clear and concise description of what the bug is.

    **To Reproduce**
    Steps to reproduce the behavior:
    1. Go to '...'
    2. Click on '....'
    3. Scroll down to '....'
    4. See error

    ```

    </details>

### Creating a Custom Form
[:hammer_and_wrench: DIY Link](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms)

 1. Add a custom template file `.github/ISSUE_TEMPLATE/custom.yml`
 2. Add a required input with a placeholder text and a label, a textarea, a single select dropdown, a multi select dropdown, and a checkbox

    <details><summary>Solution</summary>  
    
    ```yaml
    name: 💡 Custom Issue Form
    description: A custom form with different fields
    body:
      - type: input
        id: contact
        attributes:
          label: Contact Details
          description: How can we get in touch with you if we need more info?
          placeholder: ex. email@example.com
        validations:
          required: false
      - type: textarea
        id: what-happened
        attributes:
          label: What happened?
          description: Also tell us, what did you expect to happen?
          placeholder: Tell us what you see!
          value: "Tell us what you think"
        validations:
          required: true
      - type: dropdown
        id: version
        attributes:
          label: Version
          description: What version of our software are you running?
          options:
            - 1.0.2 (Default)
            - 1.0.3 (Edge)
            - 1.0.4 (Something)
        validations:
          required: true
      - type: dropdown
        id: browsers
        attributes:
          label: What browsers are you seeing the problem on?
          multiple: true
          options:
            - Firefox
            - Chrome
            - Safari
            - Microsoft Edge
      - type: checkboxes
        id: terms
        attributes:
          label: Code of Conduct
          description: By submitting this issue, you agree to follow our [Code of Conduct](https://example.com)
          options:
            - label: I agree to follow this project's Code of Conduct
              required: true
    ```
    
    </details>
    
 3. Verify your issue template and create a bug and an issue from the custom template

## Participating in Discussions
[:hammer_and_wrench: DIY Link](https://docs.github.com/en/discussions)

1. Ask a question in discussions and answer it (mark it as answered)
2. Create a poll 
3. Create an announcement
4. Pin the question and the announcement to discussion
5. See [here](https://github.com/<yourhandle>/<yourproject>/discussions) for ideas

## Rendering markdown as HTML with GitHub Pages
[:hammer_and_wrench: DIY Link](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)

1. Create a markdown file `index.md` hand add metadata `layout: home` amd some sample markdown 

<details><summary>Solution</summary> 
    
```yaml
---
layout: home
---

This is the the homepage `index.md`
```
    
</details>

2. Enable `Pages` in your repository (`main` branch - folder `/(root)` and see your new homepage
 
<details><summary>Solution</summary> 
    <img width="722" alt="image" src="https://user-images.githubusercontent.com/5276337/173327871-e3f62cf0-c101-4e6c-8911-780c779d6571.png">
</details>

3. Add a file `_config.yml` and configure pages to use the `minima` theme.

<details><summary>Solution</summary> 

```YAML
title: GitHub Bootcamp
description: >-
  This is is a sample Jekyll website that is hosted in GitHub Pages.
  It is used in the `GitHub Bootcamp` workshop from @<yourhandle>
twitter_username: <your name>
github_username: <yourhandle>
theme: minima
markdown: kramdown
```

</details>


