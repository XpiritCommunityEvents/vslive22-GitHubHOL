# 🔨 Hands-on: Setting up Code Scanning and Secret Scanning for your repository

## Objectives of this hands-on lab
This hands-on lab has the goal to teach you how you can set up Code Scanning for your repository and to let you experience how its features help you to find security vulnerabilities and code errors in the code in your repository. You will also learn how to enable Secret Scanning and will experience how it is able to scan your repository for known types of secrets and what it's capabilities are in order to prevent fraudulent use. Good luck! 👍

This hands on lab consists of the following steps:
- [🔨 Hands-on: Setting up Code Scanning and Secret Scanning for your repository](#-hands-on-setting-up-code-scanning-and-secret-scanning-for-your-repository)
  - [Objectives of this hands-on lab](#objectives-of-this-hands-on-lab)
    - [Enabling GitHub Advanced Security on your repository](#enabling-github-advanced-security-on-your-repository)
  - [Code Scanning](#code-scanning)
    - [Code Scanning: What is it?](#code-scanning-what-is-it)
    - [Enabling the Code Scanning functionality](#enabling-the-code-scanning-functionality)
    - [Analyzing Code Scanning outcomes](#analyzing-code-scanning-outcomes)
  - [Secret Scanning](#secret-scanning)
    - [Secret Scanning: What is it?](#secret-scanning-what-is-it)
    - [Enabling Secret Scanning functionality](#enabling-secret-scanning-functionality)
    - [Managing Secret Scanning alerts](#managing-secret-scanning-alerts)
      - [Secret Scanning: Alert notifications](#secret-scanning-alert-notifications)
      - [Secret Scanning: Securing compromised secrets](#secret-scanning-securing-compromised-secrets)
    - [If time permits: Triggering Secret Scanning by inserting a connection string](#if-time-permits-triggering-secret-scanning-by-inserting-a-connection-string)

### Enabling GitHub Advanced Security on your repository
Should GitHub Advanced Security not be enabled yet on your repository, you can enable it from the `Settings` menu on your repository, then under `Security & Analysis`, in the section `GitHub Advanced Security`, click `Enable`. Advanced Security should be enabled in order to enable Code Scanning and Secret Scanning.

![Advanced Security - Enable](../../images/advancedsecurityenable.PNG)

## Code Scanning
### Code Scanning: What is it?
Code scanning is a feature that you use to analyze the code in a GitHub repository to find security vulnerabilities and coding errors. Any problems identified by the analysis are shown in GitHub.

You can use code scanning to find, triage, and prioritize fixes for existing problems in your code. Code scanning also prevents developers from introducing new problems. You can schedule scans for specific days and times, or trigger scans when a specific event occurs in the repository, such as a push. If code scanning finds a potential vulnerability or error in your code, GitHub displays an alert in the repository. After you fix the code that triggered the alert, GitHub closes the alert. For more information, see [Managing code scanning alerts for your repository](https://docs.github.com/en/code-security/secure-coding/managing-code-scanning-alerts-for-your-repository]).

For GitHub Code Scanning documentation, please refer to: [https://docs.github.com/en/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/about-code-scanning](https://docs.github.com/en/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/about-code-scanning)

### Enabling the Code Scanning functionality
To enable GitHub Code Scanning, please navigate to the `Settings` of your repository, click `Security & analysis` click `Set up` for the `Code Scanning` feature.

![Code Scanning - Set up](../../images/codescanningsetup.PNG)

You'll be directed to the `Get started with Code Scanning` form, from where you can set up code scanning to use the *CodeQL Analysis* product maintained by GitHub or a third-party code scanning tool. For this lab, we'll pick the CodeQL product. To enable this, you'll click the `Set up this workflow` for the `CodeQL Analysis` product maintained by GitHub.

![Code Scanning - Get started](../../images/getstartedwithcodescanning.PNG)

After this step, a `codeql-analysis.yml` file is generated for you. For most projects, this workflow file will not need changes; you can simply commit it to your repository. 

![Code Scanning - Commit](../../images/codescanningcommit.PNG)

Once your changes are committed, you will see the `codeql-analysis.yml` file in the new directory `./github/workflows`.

![Code Scanning - CodeQL Analysis Workflow](../../images/codeqlanalysisyml.PNG)

When you click the file `codeql-analysis.yml`, you get to see the option `View runs`. 

![Code Scanning - CodeQL view runs](../../images/codeqlviewruns.PNG)

From here, you can see the list of workflows with the CodeQL workflow and the run history of the CodeQL workflow. In the default CodeQL analysis workflow, code scanning is configured to analyze your code each time you either push a change to the default branch or any protected branches, or raise a pull request against the default branch. As a result, code scanning will now commence. As you can see on the below screenshot, the workflow is currently running.

![Code Scanning - CodeQL run history](../../images/codeqlrunhistory.PNG)

After some minutes, generally around 7 to 8 minutes, the workflow run will be completed and you will see the status being updated.

![Code Scanning - CodeQL views runs (completed)](../../images/codeqlviewruns_completed.PNG)

Clicking through on the workflow run, by clicking on `Create codeql-analysis.yml`, you can see the details of the workflow run. 

![Code Scanning - CodeQL workflow completed](../../images/codeqlworkflow_completed.PNG)

Great, now that your CodeQL workflow is completed, we can move on and discover the way your Code Scanning outcomes can be analyzed. 

### Analyzing Code Scanning outcomes
When you navigate to the `Security` tab on your repository, and click `Code Scanning alerts`, you can see the active alerts for Code Scanning. From this view, you can view, fix, dismiss, or delete alerts for potential vulnerabilities or errors in your project's code.

![Code Scanning - Security Tab](../../images/codescanning_securitytab.PNG)

Each alert highlights a problem with the code and the name of the tool that identified it. You can see the line of code that triggered the alert, as well as properties of the alert, such as the severity, security severity, and the nature of the problem. Alerts also tell you when the issue was first introduced. For alerts identified by CodeQL analysis, you will also see information on how to fix the problem.

![Code Scanning - Alerts details](../../images/codescanningalertdetails.PNG)

For more detailed information on managing the Code Scanning alerts, refer to: [https://docs.github.com/en/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/managing-code-scanning-alerts-for-your-repository](https://docs.github.com/en/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/managing-code-scanning-alerts-for-your-repository)

## Secret Scanning
### Secret Scanning: What is it?
If your project communicates with an external service, you might use a token or private key for authentication. Tokens and private keys are examples of secrets that a service provider can issue. If you check a secret into a repository, anyone who has read access to the repository can use the secret to access the external service with your privileges. We recommend that you store secrets in a dedicated, secure location outside of the repository for your project.

Secret scanning will scan your entire Git history on all branches present in your GitHub repository for any secrets. Service providers can partner with GitHub to provide their secret formats for scanning. For more information, see "Secret scanning partner program."

If someone checks a secret with a known pattern into a public or private repository on GitHub, secret scanning catches the secret as it's checked in, and helps you mitigate the impact of the leak. Repository administrators are notified about any that contains a secret, and they can quickly view all detected secrets in the Security tab for the repository.

For GitHub Secret SCanning documentation, please refer to: [https://docs.github.com/en/code-security/secret-scanning/about-secret-scanning](https://docs.github.com/en/code-security/secret-scanning/about-secret-scanning)

### Enabling Secret Scanning functionality
Depending on your GitHub settings Secret Scanning may already be enabled. To turn GitHub Secret Scanning, please navigate to the `Settings` of your repository, click `Security & analysis` click `Enable` for the `Secret Scanning` feature.

![Secret Scanning - Enable](../../images/secretscanningenable.PNG)

Secret Scanning is now enabled for your repository. 

GitHub performs secret scanning on public and private repositories for secret patterns provided by GitHub and GitHub partners. However, there can be situations where you want to scan for other secret patterns in your private repositories. For example, you might have a secret pattern that is internal to your organization. For these situations, you can define custom secret scanning patterns in your enterprise, organization, or private repository on GitHub.

![Secret Scanning - Custom Patterns](../../images/secretscanningcustompatterns.PNG)

You can define up to 20 custom patterns for each private repository, organization, or enterprise account and options to define these are enabled after you enable the `Secret Scanning` feature in your `Security & analysis` settings. We'll not go into the custom patterns in this lab, but for more information refer to: [https://docs.github.com/en/code-security/secret-scanning/defining-custom-patterns-for-secret-scanning](https://docs.github.com/en/code-security/secret-scanning/defining-custom-patterns-for-secret-scanning)

Now that you've set up Secret Scanning, let's understand where you can view the Secret Scanning alerts and ultimately try it out and trigger it ourselves by inserting a connection string in the next parts of the lab exercise.

### Managing Secret Scanning alerts
When you navigate to the `Security` tab on your repository, and click `Secret Scanning alerts`, you can see the active alerts for Secret Scanning. Here, you can view and close alerts for secrets checked in to your repository.

![Secret Scanning - Alerts](../../images/secretscanningalerts.PNG)

When you click on a Secret Scanning alert, you can see it's details.

![Secret Scanning - Alert details](../../images/secretscanningalertdetails.PNG)

#### Secret Scanning: Alert notifications
When a new secret is detected, GitHub notifies all users with access to security alerts for the repository according to their notification preferences. You will receive alerts if you are watching the repository, have enabled notifications for security alerts or for all the activity on the repository, are the author of the commit that contains the secret and are not ignoring the repository.

#### Secret Scanning: Securing compromised secrets
Once a secret has been committed to a repository, you should consider the secret compromised. GitHub recommends the following actions for compromised secrets:
* For a compromised GitHub personal access token, delete the compromised token, create a new token, and update any services that use the old token. 
* For all other secrets, first verify that the secret committed to GitHub is valid. If so, create a new secret, update any services that use the old secret, and then delete the old secret.

For more information, please refer to: [https://docs.github.com/en/code-security/secret-scanning/managing-alerts-from-secret-scanning](https://docs.github.com/en/code-security/secret-scanning/managing-alerts-from-secret-scanning)

### If time permits: Triggering Secret Scanning by inserting a connection string
You can trigger the Secret Scanning functionality by inserting a secret in your repository yourself. To do so, try if you can manage to execute the following steps:
* Go to the [Azure Portal](https://portal.azure.com/)
* Create, for example, a storage account within your own subscription
* Once this is created, copy the connection string to the storage account (navigate to `Access keys`)
  ![Grab an access key from the azure portal](../../images/copy-an-access-key.png)
* Go back to your code
* Open the file `/TailwindTraders.Website/Source/Tailwind.Traders.Web/appsettings.json`, 
* At the end of the file, append the file with a `StorageAccountConnectionString` element and paste the copied connection string. 
* Commit your changes and see whether you have been able to trigger a Secret Scanning alert (give the workflow some time to run after the commit) 
