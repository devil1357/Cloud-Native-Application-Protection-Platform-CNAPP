# Module 2:   Defender for Containers

## Objectives
This exercise guides you on how to validate and use Defender for Containers.

### Exercise 1: Verify Docker Installation

1. From the **Virtual Machine** desktop, click on **Start**, and click on **Docker Desktop**.
 
    ![](images/docker1.png)

2. Complete the installation of the Docker Desktop, click on **Finish**.

    ![](images/docker2.png)

3. Click **Accept** on **Docker Subscription Service Agreement**.

    ![](images/m2-img2.png)

4. In Welcome to Docker Desktop, click on **Continue without signing in**.

    ![](images/docker3.png)

5. In the Welcome survey, Click on **Skip survey**.

    ![](images/docker4.png)

6. Wait for the **Docker Engine** to start. 

    ![](images/docker5.png)

    >**Note:** The startup process will take about five minutes. If it takes longer, restart the virtual machine.
    
7. Search for PowerShell in Search bar and select **Windows PowerShell**.

   ![Open Powershell](images/open-powershell.png)

8. Verify your docker version by executing in PowerShell. 

   ```
   docker version
   ```

   You may see an output like the one below:

   ![Docker Version in Powershell](images/docker-version.png)


### Exercise 2: Download vulnerable image from Docker Hub into the Container Registry

Now you will use Docker to download a vulnerable image from it and push it into our existing Azure Container registry.

1. Navigate to the Azure Portal, search for **Container registries** **(1)** in the search box and select **Container registries** **(2)**.

   ![Container registry in Azure](images/serach-cr1.png)

2. Open the Container Registry named **asclabcrxxxxxx**.

   ![Container registry open](images/select-cr.png)

3. In the Overview of it, verify the Login server name only. 

   ![ACR server name](images/copy-crname1.png)

4.	Switch back to PowerShell, you will also need to login to your Azure subscription via **az login**. Enter the following **Email/Username** and **Password** in the browser and click on **Sign in**:

      * Email/Username: **<inject key="AzureAdUserEmail" enableCopy="true"/>** 

      * Password: **<inject key="AzureAdUserPassword" enableCopy="true"/>**

5. Make sure to update **NameOfServer** to **<inject key="Container registry" enableCopy="true"/>** and then run the below command.
   
   ```
   az acr login --name NameOfServer
   ```
 
   ![ACR login](images/acr-login.png)

6. Download vulnerable image from docker hub, by running the command below in PowerShell:

   ```
   docker pull vulnerables/web-dvwa
   ```

   ![ACR login](images/docker-pull1.png)

7. Check the image on your local repository by running the command below:

   ```
   docker images vulnerables/web-dvwa
   ```

   ![Docker images](images/docker-pull2.png)

8. Create an alias of the image by running the following command and make sure to replace **NameOfServer** to **<inject key="Container registry" enableCopy="true"/>** and then run the below command:

   ```
   docker tag vulnerables/web-dvwa NameOfServer.azurecr.io/vulnerables/web-dvwa
   ```

9. Check again the image on your local repository by running the command and make sure to replace **NameOfServer** to **<inject key="Container registry" enableCopy="true"/>** and then run the below command:

   ```
   docker images NameOfServer.azurecr.io/vulnerables/web-dvwa
   ```

   ![Docker images](images/docker-image.png)


10. Run docker push to upload the new image to the azure repository and generate image scan (it can take some time), using the below command and make sure to replace **NameOfServer** to **<inject key="Container registry" enableCopy="true"/>** and then run the below command:

    ```
    docker push NameOfServer.azurecr.io/vulnerables/web-dvwa
    ```

    ![Docker images](images/docker-push.png)

11. Then navigate back to the Azure portal and open the Container registry named **<inject key="Container registry" enableCopy="true"/>**.

12. Now select **Repositories** **(1)** under Services in the **<inject key="Container registry" enableCopy="false"/>** Container Registry resource. Notice the **vulnerable image** **(2)** is found in the ACR repository.

    ![Image in ACR](images/cr-repos.png)

    <validation step="a9112eda-7782-494d-88f3-cd8108c7ed78" />

	  > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
	
	- Navigate to the Lab Validation Page, from the upper right corner in the lab guide section.
	- Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
	- If not, carefully read the error message and retry the step, following the instructions in the lab guide.
	- If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

### Exercise 3: Investigate the recommendation for vulnerabilities in ACR

Once a vulnerable image has been pushed to the Azure Container Registry, then Microsoft Defender for Containers will start scanning the image for vulnerabilities, by using Qualys. You will now look into the recommendation in Microsoft Defender for Cloud for this. 
 
1. In the Azure Portal, search for Microsoft Defender **(1)** in the search box and then select **Microsoft Defender for Cloud** **(2)**.

    ![Microsoft Defender](images/m2-ex3-step1.png)
   
2. From the **Microsoft Defender for Cloud** pane, select **Recommendations** from left-menu under General.

    ![Microsoft Defender](images/m2-ex3-step2.png)
 
3. Now under Secure score recommendations pane, set the **Resource type** filter to have it equal to **Container registries** **(1)** and then expand the **Remediate vulnerabilities** **(2)**. Click on the recommendation **Container registry images should have vulnerability findings resolved** **(3)** to get more details about it.  
   ![Recommendation for vulnerabilities in ACR](images/m2-ex3-step3.1.png)

4. Look around at what's available in the recommendation. Take a note of the Remediation Steps.

   ![Remediation Steps](images/m2-ex3-step4.png)
  
5. Select the vulnerability **Container registry images should have vulnerability findings resolved**, under **Security Checks**, select one of the items in the list to get additional details about the patch available for it and how to remediate it.

   ![Debian](images/m2-ex3-step5.png)
 
