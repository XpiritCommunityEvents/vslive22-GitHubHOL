# 🔨 Hands-on: Adding Traceability with releasenotes

## Objectives of this hands-on lab
This hands-on lab you will teach you how you can use GitHub to improve the traceability. By using Git as your Source Control System, you already get a lot of traceabilty out of the box. Just by committing and pushing to GitHub you create an audit trail that cannot be modified. The commit contains everything you need to conform to the traceability guidelines. However, that goes for source control. 

Sometimes organizations also want to have traceablity over their tests & releases. You can use GitHub Issues and Milestones to define your releases and tag issues in your commit messages to link issues to code commits. You can use the test reports to generate test summaries within your builds. If you want to take this one step further, you can also create releasenotes after every release you automatically create in the pipeline. 

In this exercise we are adding a GiHub action to our pipeline that generates a markdown file with release notes and publishes these release notes.. Good luck! 👍

This hands-on lab consists of the following steps:
- [🔨 Hands-on: Adding Traceability with releasenotes](#-hands-on-adding-traceability-with-releasenotes)
  - [Objectives of this hands-on lab](#objectives-of-this-hands-on-lab)
  - [Add Test Result Reports](#add-test-result-reports)
    - [Labeling our issues](#labeling-our-issues)
    - [Adding release notes](#adding-release-notes)

## Add Test Result Reports
For Compliance it is important we gather enough evidence that the software we produced also has gone through enough testing and that the test results are always available. For this we can add a step to our standard CI/CD workflow that we created previously, and also to the just created PR verification workflow.

You can add the reporting by using an action called `test-reporter` that you can find at github here: https://github.com/dorny/test-reporter

>tip: if you want to know somethign about an action used, you can always use the following URL to investigate: https://github.com/fullnameoftheaction-withoutversion

The Test reporter will generate a results overview aas part of your results step, which means the report comming out of the workflow run contains the evidence. Below is the example of adding a little step to generate the report and add it to your existing workflows:

```YAML
    - name: Test Report
      uses: dorny/test-reporter@v1
      if: success() || failure()    # run this step even if previous step failed
      with:
        name: 'Unit Tests'            # Name of the check run which will be created
        path: '**/*.trx'              # Path to test results
        reporter: 'dotnet-trx'        # Format of test results
```
Since we are using .NET, we need to make the dotnet commandline also aware of the fact we want trx reporting as the result, so it can be used by this action. fr this we need to modify the step `dotnet test` to now contain information about the logger you want to use.

Here is the new yaml you need for the test step in the workflows:
```YAML
    - name: Run tests
      working-directory: TailwindTraders.Website/Source
      run: |
        dotnet test --logger "trx;LogFileName=test-results.trx" --configuration Release
```

Make the adjustments and then you see the results in the workflow summary like here:

![Unit Test results](/images//Unit-test-results.png)


### Labeling our issues
To generate release notes without too much manual hassle, we can use issues in our GitHub repository as the base of our notes.

To easily select the issues we need, we can label the issues with a label `releasenote`.

1. In issues create a label called `releasenote`
1. Navigate to a few issues and label them with `releasenote` 

### Adding release notes
One final step that is often overlooked is that you can generate a set of release notes for the release you create. For this you can use an action that is created and can be found in our hands-on-lab repository.

This release notes action takes the input of the current owner, repo and a label name that we want to use to retrieve the releasenotes from the issues we have marked in our repository.

For this the action uses the current workflow github_token to authenticate against the github API and then it retrieves the issues that you have labeled with the label you defined.

Let assume you are the at the repository: `XpiritCommunityEvents/attendee-marcelv` and we want to use a label with the name releasenote that we use to mark our issues to show up in the release notes.

Then we can configure the CI/CD workflow we have to include the releasenotes by adding the following yaml:
```YAML
      - name: generate releasenotes
        uses: XpiritCommunityEvents/ReleasenoteAction@main
        with:
            environment: ${{ toJSON(github) }}
            owner: XpiritCommunityEvents
            repo: ReleasenoteAction
            github_token: ${{ github.token }}
            labelname: releasenote
            markdownfile: releasenotes.md
```
Assuming you have created a few issues that are labeled with in this case the label `releasenote` then the result should be visible in the build summary as show here below:

![Build summary showing release notes as part of the build](/images/releasenotes.png)
