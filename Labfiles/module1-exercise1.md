# HOL1: Exercise 1: Migrating Windows & SQL Server workloads

### Estimated time: 60 Minutes

In this HOL, you will use Azure Migrate: Server Assessment to assess the on-premises environment. This will include selecting Azure Migrate tools, deploying the Azure Migrate appliance into the on-premises environment, creating a migration assessment, and using the Azure Migrate dependency visualization.

## Lab objectives

In this HOL, you will complete the following exercises:

- Exercise 1: Migrating Windows & SQL Server Workloads
- Exercise 2: Set up your environment on Azure to Migrate Servers
- Exercise 3: Migrating your applications and data by utilizing Microsoft services and tools, such as Azure Migrate: Server Migration
- Exercise 4: Optimizing newly Migrated Workloads, and emphasizing commonalities across all Stacks

### Task 1: Discovery, Assess, and Plan: Evaluate your current environment

In this exercise, you will deploy the Azure Migrate appliance in the on-premises Hyper-V environment. This appliance communicates with the Hyper-V server to gather configuration and performance data about your on-premises VMs and returns that data to your Azure Migrate project.

1. If you are not logged in already, click on the Azure portal shortcut that is available on the desktop and log in with the below Azure credentials.
    
    - Enter your Username/Email: <inject key="AzureAdUserEmail"></inject> in the Sign in field. Click Next to continue.
      
      ![](./Images/614-7-25-g6.png)
      
    - Enter Password: <inject key="AzureAdUserPassword"></inject> and click Sign in

      ![](./Images/614-7-25-g7.png)

1. In the Azure portal, click the **Show Portal Menu (1)** icon, then select  **All services (2)** from the left navigation pane.
 
    ![Screenshot of the All services overview blade.](Images/15-7-25-1.png "All services Overview blade")

1. In the search bar at the top of the Azure portal, type **Azure Migrate (1)**, and select **Azure Migrate (2)** from the Services section.
 
    ![Screenshot of the Azure migrate overview blade.](Images/15-7-25-l1-1.png "Azmigrate Overview blade")

1. On the **Azure Migrate** | Servers, databases and web apps page, select **Servers, databases and web apps (1)** under **Migration goals** from the left panel, and then under **Azure Migrate: Discovery and assessment**, select **Discover (2)** -> **Using appliance (3)** to open the Discover blade.
 
    ![](Images/15-7-25-l1-2.png)
 
1. On the **Discover** page, under **Are your servers virtualized?**, click the drop-down **(1)** and select **Yes, with Hyper-V (2)** from the list.

    ![](Images/15-7-25-l1-3.png)

1. On the **Discover page**, under **1: Generate project key**, enter the name below as the appliance name **(1)**, then click **Generate key (2)** to start creating the required Azure resources.

     ```
     SmartHotelAppl
     ```
    ![Screenshot of the Azure Migrate 'Discover machines' blade showing the 'Generate Azure Migrate project key' section.](Images/15-7-25-l1-4.png "Generate Azure Migrate project key")

1. Once the project key is generated, click the **copy** icon to the right of the **Project key** field and save it in a Notepad for future reference.

    ![Screenshot of the Azure Migrate 'Discover machines' blade showing the Azure Migrate project key.](Images/15-7-25-l1-5.png "Azure Migrate project key")

1.  Read through the instructions on how to download, deploy, and configure the Azure Migrate appliance, then close the 'Discover machines' blade by clicking on the cross button **X** (do **not** download the .VHD file or .ZIP file, the .VHD has already been downloaded for you). 
 
    ![Screenshot of the closing the blade.](Images/15-7-25-l1-6.png "Closing the Azure migrate appliance blade")

1. As we have created the Azure Migrate project key for the Discover and Assessment, you will be accessing the Hyper-V manager in the next tasks to start the discovery process with the help of the Azure Migrate Appliance.

1. On the lab VM, click the **Start (1)** button, search for **Hyper-V Manager (2)**, and select  **Hyper-V Manager (3)** from the results. You will use Hyper-V Manager to access your infrastructure and connect to the Azure Migrate Appliance VM to begin discovery.

    > You can also open the Hyper-V Manager by clicking on the ![](Images/Icon-hyperv.png) icon in the taskbar.

      ![Screenshot of Hyper-V Manager, with the 'Hyper-V Manager' action highlighted.](Images/15-7-25-l1-7.png "Hyper-V Manager")

1. In Hyper-V Manager, select **HOSTVMS<inject key="DeploymentID" enableCopy="false" /> (1)** from the left pane. You should now see the AzureMigrateAppliance VM along with other VMs **(2)** that make up the on-premises SmartHotel application and will be used in upcoming hands-on labs.

    ![Screenshot of Hyper-V Manager on the SmartHotelHost.](Images/15-7-25-l1-8.png "Hyper-V Manager")
     
1. In Hyper-V Manager, select the **AzureMigrateAppliance (1)** VM, then click **Start (2)** from the right-hand Actions pane if it is not already running.

    ![Screenshot of Hyper-V Manager showing the start button for the Azure Migrate appliance.](Images/HOL1-EX1-S12.png "Start AzureMigrateAppliance")
    
     > **Note:** If you encounter an error while starting the **AzureMigrateAppliance** VM, try **turning off** the **AzureArcVM**, then start the **AzureMigrateAppliance** VM again.

1. In Hyper-V Manager, select the **AzureMigrateAppliance (1)** VM, then click **Connect (2)** from the right-hand Actions pane.

    ![Screenshot of Hyper-V Manager showing the connect button for the Azure Migrate appliance.](Images/15-7-25-l1-9.png "Connect to AzureMigrateAppliance")    
   
1. On the **Connect to AzureMigrateAppliance** window, click **Connect**, then log in to the VM using the administrator password: **<inject key="SmartHotel Admin Password" />** (Note: The login screen may use your local keyboard layout, click the 'eyeball' icon to verify your password.)
 
    ![Screenshot of the Connect to AzureMigrateAppliance.](Images/15-7-25-l1-10.png)

    ![Screenshot of the Connect to AzureMigrateAppliance.](Images/15-7-25-l1-11.png)

1. On the desktop of the AzureMigrateAppliance VM, double-click the **Azure Migrate Appliance Configuration Manager** shortcut to launch the wizard. Wait a minute or two for the browser to open and display the configuration wizard.

     > **Note:** If a New updates available pop-up appears, click View updates, then close the settings panel. You can proceed without applying the updates for now.

    ![Screenshot of the Azure Migrate appliance terms of use.](Images/15-7-25-l1-12.png)
    
    >**Note:** If you receive a prompt asking for credentials after launching the **Azure Migrate appliance configuration wizard** from the desktop shortcut, follow the instructions [here](https://github.com/CloudLabsAI-Azure/Know-Before-You-Go/blob/main/AIW-KBYG/AIW-Infrastructure-Migration.md#1-exercise1---task3---step3) to connect to the appliance configuration wizard.

1. If a **Terms of use** pop-up appears in the appliance configuration wizard, review the license terms and click **I agree** to accept.

    ![Screenshot of the Azure Migrate appliance terms of use.](Images/15-7-25-l1-13.png "Terms of use")

1. On the **Appliance Configuration Manager Cloud: Public** page, under **Set up prerequisites**, the following two checks, **Check connectivity to Azure** and **Check time is in sync with Azure**, should pass automatically.

    ![Screenshot of the Azure Migrate appliance configuration wizard, showing the first step 'Set up prerequisites' in progress. The internet connectivity and time sync steps have been completed.](Images/15-7-25-l1-14.png)

1. On the **Appliance Configuration Manager Cloud: Public** page, under **1. Set up prerequisites**, expand **Check latest updates and register appliance**. Paste the **Azure Migrate project key (1)** that you copied earlier, then click **Verify (2)** to validate the key.

    ![Screenshot of the Azure Migrate appliance configuration wizard, showing the registration with the Azure Migrate project.](Images/15-7-25-l1-15.png "Register with Azure Migrate")

1. **Wait** while the wizard installs the latest Azure Migrate updates. If prompted, log in using the credentials, enter username as **Administrator** and password **<inject key="SmartHotel Admin Password" />**. Once the update completes, if a **New update installed** pop-up appears, click **Refresh** to restart the appliance management app.

    ![Screenshot of the Azure Migrate appliance configuration wizard, showing the prompt to restart the management app after installing updates.](Images/15-7-25-l1-16.png "New update installed - Refresh")

1. Under **Check latest updates and register appliance**, wait for the **Appliance auto-update status (1)** to show successful completion. This may take up to **5 minutes**. Once completed, click **Login (2)** to sign in with your Azure credentials.

    ![Screenshot of the Azure Migrate appliance configuration wizard, showing the registration with the login code for the Azure Migrate project.](Images/15-7-25-l1-17.png)
   
    >**Note:** Now, follow the instructions below to complete the login process.
    
 1. After clicking Login, the **Continue with Azure Login** pop-up dialog, click **Copy code & Login** to copy the device code.
    
    ![Screenshot of the Azure Migrate appliance configuration wizard, showing the registration with the login code for the Azure Migrate project.](Images/15-7-25-l1-18.png "Azure Migrate login code")
  
 1. This will open an Azure login prompt in a new browser tab. If it doesn’t appear, ensure that your browser’s pop-up blocker is disabled. Paste the device **code (1)** and click **Next (2)**. You will then be prompted to sign in with your Azure portal credentials to complete the login.

     ![Screenshot of the Azure Migrate appliance login window, showing where to copy and paste the login code for the Azure Migrate project.](Images/15-7-25-l1-19.png "Azure Migrate Microsoft login")

 1. Log in using the provided Azure credentials. On the **Are you trying to sign in to Microsoft Azure PowerShell?** prompt, select **Continue to complete the login**. 
    
     - Azure Username/Email: <inject key="AzureAdUserEmail"></inject>
        
        ![](Images/15-7-25-l1-20.png)
       
     - Azure Password: <inject key="AzureAdUserPassword"></inject>
   
        ![](Images/15-7-25-l1-21.png)

        ![](Images/15-7-25-l1-22.png)
       
1. Once signed in, return to the Azure Migrate Appliance tab—the appliance registration will begin automatically and display The appliance has been successfully registered once complete.

   ![Screenshot of the Azure Migrate appliance configuration wizard, showing the registration with the Azure Migrate project as completed.](Images/15-7-25-l1-23.png "Appliance registered")

1. Once registration is complete, navigate to the **Manage credentials and discovery sources** panel. Under **Step 1: Provide Hyper-V host credentials for discovery of Hyper-V VMs**, click **Add credentials** to proceed.

    ![Screenshot of the Azure Migrate appliance configuration wizard, showing the 'Add credentials' button.](Images/15-7-25-l1-24.png)

1. On the **Add credentials** tab, enter the following details for the Hyper-V host/cluster that the appliance will use to discover VMs, and then click **Save (4)** to continue.
 
      - Friendly name: Enter **hostlogin (1)** 
      - Username: **<inject key="SmartHotelHost Admin Username" /> (2)**
      - Password: **<inject key="SmartHotelHost Admin Password" /> (3)**

        ![Screenshot of the Azure Migrate appliance configuration wizard, showing the 'Add credentials' panel.](Images/15-7-25-l1-25.png "Credentials")

        > **Note**: The Azure Migrate appliance may not have picked up your local keyboard mapping. Select the 'eyeball' in the password box to check that the password was entered correctly.

1. In **Step 2: Provide Hyper-V host/cluster details**, click **Add discovery source** to specify the IP address or FQDN of the Hyper-V host/cluster
   
    ![Screenshot of the Azure Migrate appliance configuration wizard, showing the 'Add discovery source' button.](Images/15-7-25-l1-26.png "Add discovery source")

1. On the **Add discovery source** blade, provide the following details:
     
      - Select **Add single item (1)**
      - IP Address / FQDN:  Enter **HOSTVMS<inject key="DeploymentID" enableCopy="false" /> (2)** 
      - Friendly name: Select **hostlogin (3)** from the dropdown and 
      - Select **Save (4)**.

        ![Screenshot of the Azure Migrate appliance configuration wizard, showing the 'Add discovery source' panel.](Images/15-7-25-l1-27.png "Discovery source - SmartHotelHost")

         > **Note:** You can either **Add single item** at a time or **Add multiple items** in one go. There is also an option to provide Hyper-V host/cluster details through **Import CSV**.

1. Once the discovery source is added, the appliance will validate the connection to the Hyper-V host/cluster. A **Validation successful** status will be displayed in the table next to the corresponding host or cluster.

    ![Screenshot of the Azure Migrate appliance configuration wizard, showing the successful validation of the configured discovery source.](Images/15-7-25-l1-28.png "Discovery source - validation successful")

    > **Note:** When adding discovery sources:
    > - For successfully validated hosts/clusters, you can view more details by selecting their IP address/FQDN.
    > - If validation fails for a host, review the error by selecting Validation failed in the Status column of the table. Fix the issue and validate again.
    > - To remove hosts or clusters, select **Delete**.
    > - You can't remove a specific host from a cluster. You can only remove the entire cluster.
    > - You can add a cluster, even if there are issues with specific hosts in the cluster.

1. In **Step 3: Provide server credentials to perform software inventory and agentless dependency analysis**, **Disable the slider**, and then select **Start discovery**  to begin VM discovery from the validated Hyper-V hosts or clusters.

   >**Note:** The discovery process may take up to 10 minutes to complete
   
   ![](Images/15-7-25-l1-29.png)
    
   ![](Images/15-7-25-l1-30.png)

1. Wait for the Azure Migrate status to show that **Discovery has been successfully initiated**. This will take several minutes. After the discovery has been successfully initiated, you can check the discovery status against each host/cluster in the table. (Wait for the Azure Migrate status to display . Discovery has been successfully initiated. This may take several minutes. Once initiated, you can view the discovery status for each host or cluster in the table.)
  
1.  Return to the **JumpVM**, then navigate to the **Azure Migrate** page in the Azure portal. Under **Migration goals**, select **Servers, databases and web apps (1)**, then click **Refresh (2)**. In the **Azure Migrate: Discovery and assessment** panel, you should see a count of **Discovered servers (3)**. If discovery is still in progress, continue clicking Refresh periodically until all 7 servers are shown. This may take several minutes.

    ![](Images/15-7-25-l1-31.png) 

    > **Note:** **Wait for the discovery process to complete before proceeding to the next Task**.

### Summary 

In this exercise, you explored an Azure Migrate project and the default built-in tools for server assessment and server migration. You have also configured the Azure Migrate appliance in the on-premises Hyper-V environment and started the migration assessment discovery process using Azure Migrate.

Click on **Next >>** from the lower right corner to move on to the next page.

![](Images/14-next.png)
