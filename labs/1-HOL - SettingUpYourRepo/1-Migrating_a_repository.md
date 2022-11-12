# 🔨 Hands-on: Import an existing repository to GitHub

## Objectives of this hands-on lab
This hands-on lab has the objective to show you how you can migrate an existing git repository to GitHub. At the end of this hands-on lab, your GitHub repository (`https://github.com/XpiritCommunityEvents/attendee-<yourGitHubhandle>`) will contain a migrated copy of an existing repository that we have prepared for this exercise. This is the first step that needs to be finished for all the other labs to succeed, as you will use this repository to perform the other hands-on labs. Good luck! 👍

This hands-on lab consists of the following steps:
- [🔨 Hands-on: Import an existing repository to GitHub](#-hands-on-import-an-existing-repository-to-github)
  - [Objectives of this hands-on lab](#objectives-of-this-hands-on-lab)
    - [Acquiring the GitHub repository URI](#acquiring-the-github-repository-uri)
    - [Import the repository using the command-line(advanced)](#import-the-repository-using-the-command-lineadvanced)
      - [Authentication](#authentication)
        - [HTTPS Authentication](#https-authentication)
        - [SSH Authentication](#ssh-authentication)
    - [Push to attendee repository](#push-to-attendee-repository)

### Acquiring the GitHub repository URI
For this bootcamp, we have prepared a demo repository for you and created a private GitHub repository for you. Before you can clone the existing repository, you'll need an URI that points to the existing repository. This URI represents the source of the repo you're going to copy. 

**For this bootcamp, please use the following clone URL: [https://github.com/XpiritCommunityEvents/vslive2022-tailwind](https://github.com/XpiritCommunityEvents/vslive2022-tailwind.git)**

Start with retrieving the Clone URL of the GitHub repository you want to migrate.
1. From your web browser, navigate to your own repository. You will see an empty repo
2. Add the bottom of the screen you will see a button `Import code`
3. In the next screen, paste the clone url of the source repo `https://github.com/XpiritCommunityEvents/vslive2022-tailwind.git`
4. Press "Begin Import" to start the import process


### Import the repository using the command-line(advanced)

In this step, you clone the repository locally, then push it into GitHub. This requires the Git client, which you can [download here](https://git-scm.com/download/gui/windows).

Start a command prompt and move to a location where you want to clone the repo on your machine, e.g. `c:\sources`. 

Enter the following command and make sure you read the [Authentication](#authentication) part below.

``` powershell
git clone [PASTE_CLONE_URL_HERE] 
```

#### Authentication
Since we are using a `Private` repository, you need to authenticate your session. If you have installed Git for Windows with the Credential Manager option, this information will be stored on your machine after authenticating for the first time. 

For the authentication you can either use SSH or HTTPS. 

##### HTTPS Authentication
If you are using HTTPS then you need to create a Personal Access Token (PAT). Go to [https://github.com/settings/tokens](https://github.com/settings/tokens) to create one. Give it the `Full control of private repositories` scope and a meaningful note. Store the token somewhere safe, it will only be visible once!  

The username in the authentication prompt can be anything, since it will not be used. For the password: enter the PAT.

##### SSH Authentication
For SSH authentication you need to add your public key by going to [https://github.com/settings/keys](https://github.com/settings/keys).


### Push to attendee repository 
Now we have a cloned repository with the full history on your local drive. Next, we want to move this repo with the history to the GitHub repo that is available for you.
You should have access to a GitHub Repo in the organization [https://github.com/XpiritCommunityEvents](https://github.com/XpiritCommunityEvents). This repo has the name `attendee-<your-github-handle>`

Now, we'll change the remote to your GitHub repository. To achieve this, you use these commands: 

``` powershell
cd demo
git remote remove origin
git remote add origin {your personal repo clone uri}
```

So, your command would look something like `git remote add origin https://github.com/XpiritCommunityEvents/attendee-<your-github-handle>.git`

Now we are ready to push the complete repo, including it's history, branches and tags to the GitHub repo.
For this you can use the command:

``` powershell
git push origin
```

> NOTE: In case you had already initialized your repo over on GitHub, you can force the code into the repo by adding `-f`. **This will overwrite your repository and its contents!**
> 
> ``` powershell
> git push -f origin
> ```

The repository is now migrated to your GitHub repo with full history. 

