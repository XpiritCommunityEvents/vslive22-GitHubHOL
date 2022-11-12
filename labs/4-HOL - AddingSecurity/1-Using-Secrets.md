# 🔨 Hands-on: Making your Deployment Workflows more secure

## Objectives of this hands-on lab
This hands-on lab has the goal to teach you how you can prevent committing secrets into your repository so they are kept more secret!
For this you are going to use GitHub secrets

## Changing the deploy job
Open the action workflow file that contains the action workflow we created in the previous labs.
In the deploy job, you use a GitHub action that you pass in a full publishing profile. We are going to move this to GitHub secrets.

This is the section we are refering to:
```YAML
deploy:
    runs-on: ubuntu-latest
    needs: build
    environment: staging
    steps:
      - name: Download artifact from build job
        uses: actions/download-artifact@v2
        with:
          name: .net-app
          
      - name: Deploy to Azure Web App
        id: deploy-to-webapp
        uses: azure/webapps-deploy@v2
        with:
          app-name: 'Tailwind-vslive'
          publish-profile: '<publishData><publishProfile profileName="Tailwind-vslive - Web Deploy" publishMethod="MSDeploy" publishUrl="tailwind-vslive.scm.azurewebsites.net:443" msdeploySite="Tailwind-vslive" userName="$Tailwind-vslive" userPWD="5mCyEWmuEu81muTRvm1Li0cLLCuJcSZjLaiMQjeSkW8nFFn8WE4rT4Nahm0H" destinationAppUrl="https://tailwind-vslive.azurewebsites.net" SQLServerDBConnectionString="" mySQLDBConnectionString="" hostingProviderForumLink="" controlPanelLink="http://windows.azure.com" webSystem="WebSites"><databases /></publishProfile><publishProfile profileName="Tailwind-vslive - FTP" publishMethod="FTP" publishUrl="ftps://waws-prod-dm1-301.ftp.azurewebsites.windows.net/site/wwwroot" ftpPassiveMode="True" userName="Tailwind-vslive\$Tailwind-vslive" userPWD="5mCyEWmuEu81muTRvm1Li0cLLCuJcSZjLaiMQjeSkW8nFFn8WE4rT4Nahm0H" destinationAppUrl="https://tailwind-vslive.azurewebsites.net" SQLServerDBConnectionString="" mySQLDBConnectionString="" hostingProviderForumLink="" controlPanelLink="http://windows.azure.com" webSystem="WebSites"><databases /></publishProfile><publishProfile profileName="Tailwind-vslive - Zip Deploy" publishMethod="ZipDeploy" publishUrl="tailwind-vslive.scm.azurewebsites.net:443" userName="$Tailwind-vslive" userPWD="5mCyEWmuEu81muTRvm1Li0cLLCuJcSZjLaiMQjeSkW8nFFn8WE4rT4Nahm0H" destinationAppUrl="https://tailwind-vslive.azurewebsites.net" SQLServerDBConnectionString="" mySQLDBConnectionString="" hostingProviderForumLink="" controlPanelLink="http://windows.azure.com" webSystem="WebSites"><databases /></publishProfile></publishData>'
          package: .
```
Remove the profile and copy this string to the clipboard.
Next go to the GitHub settings page where you can add a secret for actions in your repository. This is shown the below screenshot:
![add secret](/images/2022-11-12-15-51-33.png)
Choose New Repository Secret and give the secret the name `Azure_WebApp_PublishingProfile` and pass the contents in the value field.

> Note the moment you save the secret, you can not retrieve it in the UI of github and it will be obfuscated in the logs.

Change variable assignment in the actions workflow and use an expression syntax to refer to the secret. You can use the `SECRETS` context and then the name you provided for the secret. In our case the full expression is `${{SECRETS.Azure_WebApp_PublishingProfile}}`

The result is as follows:

```YAML
deploy:
    runs-on: ubuntu-latest
    needs: build
    environment: staging
    steps:
      - name: Download artifact from build job
        uses: actions/download-artifact@v2
        with:
          name: .net-app
          
      - name: Deploy to Azure Web App
        id: deploy-to-webapp
        uses: azure/webapps-deploy@v2
        with:
          app-name: 'Tailwind-vslive'
          publish-profile: ${{SECRETS.Azure_WebApp_PublishingProfile}}
          package: .
```

Save the workflow and run the workflow to see if the deployment still succeeds.

:thumbsup: Congratulations, you made a good step in securing your secrets!