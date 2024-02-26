# Module 2:  Configuring Azure ADO Connector in Defender for DevOps

## Objectives
In this exercise, you will learn how to configure Azure ADO Connector in Defender for DevOps.

### Exercise 1: Configuring Azure ADO Connector
In this exercise you will create a new Azure DevOps organization.

1. Navigate to [Azure DevOps](https://dev.azure.com) and login using the following credentials:

    * Email:  **<inject key="AzureAdUserEmail" enableCopy="true"/>** 
    * Password:  **<inject key="AzureAdUserPassword" enableCopy="true"/>**

2. Click on **Organization settings**. 

    ![](images/m3-img6.png)

3. Next, select **Policies (1)** under **Security** and set the toggle button **On** for **Third-party application access via OAuth (2)** and **Allow public projects (3)**. Then click **Save (4)** on **Change policy setting** pop-up.

    ![](images/m3-img46.png)

    ![](images/m3-img47.png)

4. Click on **Azure Devops (1)** to navigate back to the home page. In the **Create a project to get started** pane, enter the **Project name** as **ODL_User_<inject key="Deployment ID" enableCopy="false"/> (2)** set **Visibility** to **Public (3)** and click **+ Create project (4)**. 

    ![](images/m3-img48.png)

5. Navigate to **Microsoft Defender for Cloud** on the **Azure Portal**. Click on **Environment Settings (1)** click the **Add environment (2)** button and click **Azure DevOps (3)** option. 

    ![](images/m3a-img1.png)

6. Enter the **Connector name** for the connector as `CNAPP-Devops` **(1)**, select your **Subscription (2)**, select **asclab (3)** resource group, select any **Region (3)**. Select **Next : Select plans > (5)**.

    ![](images/m3a-img2.png)

7. In the next page leave the default selection with **DevOps** selected and click **Next: Configure access >** button to continue. 

    ![](images/m3a-img3.png)

8. Click **Authorize** button. If this is the first time you’re authorizing your DevOps connection, you’ll receive a pop-up screen, that will ask your permission to authorize. Scroll down the pop-up window screen and click the **Accept** button as shown in the sample below:

    ![](images/m3a-img4.png)

    ![](images/m3-img5.png)

   > **Note**: When you click **Accept** in your Azure DevOps, you’ll notice the proof of Authorization to the **Microsoft Security DevOps** App. You can find this in your Azure ADO organization, under the **Personal Access tokens** / **User Settings** / **Authorizatons**.  

9. After the authorization is complete, select **All existing and future organizations (1)**.	Click **Review and genrate (2)** button to continue.

      ![](images/m3a-img8.png)

10. Click on **Create**.

      ![](images/m3a-img9.png)
      
11. After some minutes you will see the Azure DevOps connector in the **Environment settings** page and in about 15 minutes, you will start to seeing the total resources number populating.

      ![](images/m3-img49.png)

### Exercise 2: Configure the Microsoft Security DevOps Azure DevOps Extension

1.	Navigate back to [Azure DevOps](https://dev.azure.com) tab open in your browser. In the right corner, click in the **Shopping bag icon (1)** and click **Browse marketplace (2)** option.

      ![](images/m3-img10.png)

2.	In the marketplace search and select **Microsoft Security DevOps** extension.  

      ![](images/m3-img11.png)

3.	Next click on **Get it free**.

      ![](images/m3-img12.png)

4. Choose your **Organization (1)** from the dropdown menu, select **Install (2)**.

      ![](images/m3-img13.png)

5. Click on **Proceed to Organization**. 

     ![](images/m3-img14.png)

6. From **Organization settings**, click on **Extensions (1)** under **Installed (2)** extensions you can view the **Microsoft Security DevOps (3)** extension that is installed. 

      ![](images/m3-img15.png)

    >**Note** Admin privileges to the Azure DevOps organization are required to install the extension. If you don’t have access to install the extension, you must request access from your Azure DevOps organization’s administrator during the installation process.


### Exercise 3: Install Free extension SARIF SAST Scans Tab

In order to view the scan results (when you execute the pipelines), in an easier and readable format, install this free extension in your Azure DevOps organization.

1. In **Azure DevOps** from the right corner, click in the **Shopping bag icon (1)** and click **Browse marketplace (2)** option.

      ![](images/m3-img10.png)
     
2. In the marketplace search and select **SARIF SANST Scans** extension.

      ![](images/m3-img16.png)

3. Next click on **Get it free**.

      ![](images/m3-img17.png)

4. Choose your **Organization (1)** from the dropdown menu, select **Install (2)**.

     ![](images/m3-img18.png)

5. Click on **Proceed to Organization**. 

     ![](images/m3-img19.png)

6. From **Organization settings**, click on **Extensions (1)** under **Installed (2)** extensions you can view the **SARIF SANST Scans (3)** extension that is installed. 

     ![](images/m3-img20.png)


### Exercise 4: Create a Hosted Build Agent and Pipeline

1. In the **Azure Portal**, click in the search bar, type **vmss** and then click **Virtual machine scale sets**. 

     ![](images/m3-img21.png)

2. Click **Create** button.

     ![](images/m3-img22.png)

3. In the Create a virtual machine scale set page, select your **Subscription (1)**, select **asclab (2)** resource group, provide the **Virtual machine scale set name** as `build-agent` **(3)**, for **Region** select **<inject key="Resource group Location" enableCopy="false" /> (4)**, for **Orchestration mode** select **Uniform (5)** leave all other options as is and change the image to **Windows Server 2022 Datacentre: Azure Edition Core - x64 Gen2 (6)**.

     ![](images/m3-img50.png)

4. In the same page, enter the following username and password for **VMSS** and click **Networking** tab.

    - **Username**: `demouser` 
    - **Password**: `demo!pass123`
    - **Confirm password**: `demo!pass123`

     ![](images/m3-img24.1.png)

5. In the Networking tab, click on **Edit** under **Network Interface**.

     ![](images/m3-img53.png)

6. In **Edit Network Interface** tab, set the toggle button to **Enabled** for **Public IP address (1)** and click on **OK**.

     ![](images/editnic.png)

7. Once you are back on the **Networking** tab click **Review + Create**.

     ![](images/m3-img55.png)

8. In the next page, you should see that all the validation are passed and now you can click **Create** button. The deployment will take a few minutes to complete.

     ![](images/m3-img51.1.png)

9. Once the deployment is completed, click on **Go to resource** button.

     ![](images/m3-img26.png)

10. In the **build-agent** page, click on **Instances** option in the left. Confirm that the build-agents are **Running**. 

     ![](images/m3a-img27.png)

11. Navigate to **build-agent_1** and click on **Network Setting (1)**, click on **create port rule (2)** and select **inbound port rule (3)**.

     ![](images/addport1.png)

12. Enter `3389` **(1)** under **Destination port range** and click **Add (2)**.
     
     ![](images/rdp.png)

13. From the **Overview (1)** page, copy the **Public IP address (2)** and paste in a text editor like ***Notepad***.
   
     ![](images/copyip.png)

14. On your **Labvm**, search for **rdp** in windows search and select **Remote Desktop Connection**.

     ![](images/rdplog.png)
 
15. Enter the **IP** you copied earlier and click **Connect**.

     ![](images/ip.png)

16. Enter the following credentials and click **OK**.

    - **Username**: `.\demouser` 
    - **Password**: `demo!pass123`

     ![](images/userpwd.png)

17. Once you enter the remote session, search for **powershell** in windows search and select **Powershell ISE**.

     ![](images/powershellise.png)

18. Paste the following commands to install ***nodejs (1)*** and click on **Run (2)** button. 

     ```
    #Install nodejs v16.8.0
    $WebClient = New-Object System.Net.WebClient
    $WebClient.DownloadFile("https://nodejs.org/download/release/v16.8.0/node-v16.8.0-x64.msi","C:\node-v16.8.0-x64.msi")
    $arguments = "/i `"C:\node-v16.8.0-x64.msi`" /quiet"
    Start-Process msiexec.exe -ArgumentList $arguments -Wait
    sleep 5
      ```

     ![](images/nodejs1.png)
     
19. Next, in the windows search bar type ***cmd*** and select **Command Prompt**.

     ![](images/cmd1.png)

20. In the command prompt, run the following npm command.

      ```
      npm.cmd install --loglevel error eslint@7.32.0 typescript@4.3.2 @microsoft/eslint-plugin-sdl@0.1.7 eslint-plugin-react@7.24.0 eslint-plugin-security@1.4.0 @typescript-eslint/typescript-estree@4.27.0 @typescript-eslint/parser@4.27.0 @typescript-eslint/eslint-plugin@4.27.0 @microsoft/eslint-formatter-sarif@2.1.5 eslint-plugin-node@11.1.0 --prefix C:\a\_msdo\packages\node_modules\eslint –global
      ```
     
     ![](images/npm1.png)

21. Close the **RDP** session by clicking on **X**.

     ![](images/close.png)

22. Navigate to [Azure DevOps](https://dev.azure.com), in the main page, click on your **Project**.

     ![](images/m3-img28.png)


23. In the bottom of left navigation page, click **Project settings** option.

     ![](images/m3-img29.png)

24. In the left navigation page, under **Pipelines** section, click **Agent pools (1)** option. From the top right corner of the page, click **Add pool (2)** button.

     ![](images/m3-img30.png)

25. In the **Add agent pool** page, click on the drop down list and select **Azure virtual machine scale set**.

     ![](images/m3-img31.png)

26. Select your **subscription (1)** and click **Authorize (2)** button.

     ![](images/m3-img32.png)

27. After the authorization is done, click on the virtual machine scale set drop-down list and select **build-agent (1)**. Under the **Name** field, enter **windows-build-agents (2)**.

     ![](images/m3-img33.png)
     >**Note: You may get an error about client not allowed, click button with circle (refresh) to fix**.

28. Enter `1` under **Maximum number of virtual machines in the scale set (1)** and **Number of agents to keep on standby (2)** fields then check the box next to **Grant access permission to all pipelines (3)** and click **Create (4)**.

     ![](images/m3-img52.png)

29. In the **Agent pools** page, you can view newly created pool.

     ![](images/m3-img35.png)

30. Navigate back to **Azure Portal**, on the **VMSS** page click on **Instances (1)** from the left menu, select both the **Build Agents (2)** and click **Upgrade (3)**.

     ![](images/upgradeinst.png)

### Exercise 5: Configure your pipeline using YAML 

The purpose of this exercise is to allow you to see how the extension used by Defender for DevOps will check your pipeline.

1.	Login to the GitHub using the following URL on the **Labvm**, by fetching the details from **Environment Details (1)** page on the right tab, click on **Licenses (2)** tab and copy the **GitHub credentials (3)**.

      ```
      https://github.com/
      ```

      ![](images/gitcred.png)

2. For Device Verification Code, use the same credentials as in the previous step, open http://outlook.office.com/ in a private window and enter the same username and password used for GitHub Account login. Copy the verification code and Paste code it in Device verification.

   ![](images/email-verify.png)

3. Navigate to following Git Repository **(1)** and click on **Fork (2)**.
   
      ```
      https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main
      ```
     
    ![](images/m4-img22.png)

4. In **Create a new fork**, disable **Copy the main branch only (1)** and click **Create fork (1)**. 

      ![](images/m4-img23.png)

5. Once the repository is forked click on **Code (1)** and copy the **URL (2)**. Paste into any text editor like *Notepad*.

      ![](images/giturl.png)

6. Login to the **Azure DevOps**(https://dev.azure.com) and open your **Project**.

     ![](images/m3-img28.png)

7. From the left pane, click on **Repos (1)** and click **Import (2)** under **Import a repository**.

     ![](images/importrepo.png)

8. On the **Import a Git repository** pane, for **Clone URL (1)** paste the **URL** you copied the previous, then click **Import (2)**.

     ![](images/gitimport.png)

9. Next, in the left navigation pane, click **Pipelines (1)**. In the right pane, click **Create Pipeline (2)** button.

     ![](images/m3-img36.png)

10. In the **Where is your code?** page, click **Azure Repos Git**.

     ![](images/m3-img37.png)

11. Click on the existing **Repository**.

     ![](images/m3-img38.png)

12. In the **Configure your pipeline** page, replace the **YAML code (1)** for the one below and click **Save and run (2)** :

      ```
      # Starter pipeline
      # Start with a minimal pipeline that you can customize to build and deploy your code.
      # Add steps that build, run tests, deploy, and more:
      # https://aka.ms/yaml
      trigger: none
      pool: windows-build-agents
      steps:
      - task: UseDotNet@2
        displayName: 'Use dotnet'
        inputs:
          version: 3.1.x
      - task: UseDotNet@2
        displayName: 'Use dotnet'
        inputs:
          version: 5.0.x
      - task: UseDotNet@2
        displayName: 'Use dotnet'
        inputs:
          version: 6.0.x
      - task: MicrosoftSecurityDevOps@1
        displayName: 'Microsoft Security DevOps'
      ```
     
      ![](images/m3-img39.png)

      > **Note**: Observe that the pool is pointing to windows-build-agents, which is the VMSS that you created.

13. Click the **Save and run** button again.

      ![](images/m3-img40.png)

    > **Note**: At this point the job will queue up to run. This step may take some time to spin up a build agent in the VMSS. During this time, if you go back to VMSS dashboard you will see that the instance is getting created.

14. In a few more minutes, the job will start to have some activity as shown the example below:

      ![](images/m3-img44.png)

15. Once it finishes you can see scan done by Defender for DevOps. To do that click **Microsoft Security DevOps** section in the left and you will see the output of the actions that were done as shown below:

      ![](images/m3-img45.png)



