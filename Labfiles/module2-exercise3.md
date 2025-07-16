
# HOL2: Exercise 3: Migrating your applications and data using Microsoft services and tools, such as Azure Migrate, the Azure Hybrid Benefit, and additional programs


### Estimated time: 50 minutes

In this exercise, you will review the registered Hyper-V host, LabVM, using Azure Site Recovery as the migration engine. The Azure Site Recovery Provider was deployed in a previous hands-on lab. Next, configure and enable replication of on-premises virtual machines from Hyper-V to the Azure Migrate Server Migration service. Modify settings for replicated virtual machines to align with on-premises IP addresses. Finally, execute the migration of the Red Hat virtual machine to Azure for a seamless transition to the cloud environment.

## Lab objectives

In this exercise, you will complete the following tasks:

- Task 1: Register the Hyper-V Host with Migration and modernization
- Task 2: Enable Replication from Hyper-V to Azure Migrate
- Task 3: Configure Networking
- Task 4: Server migration

## Task 1: Register the Hyper-V Host with Migration and modernization

In this task, you will review the already registered Hyper-V host(LabVM) with the Migration and modernization service. This service uses Azure Site Recovery as the underlying migration engine. As part of the registration process, we have already deployed the Azure Site Recovery Provider on your Hyper-V host in HOL1 and we will be using the same here as well.

1. Return to the **Azure Migrate | Servers, databases and web apps** page in the Azure Portal, expand **Migration goals (1)** on the left menu and select **Servers, databases and web apps (1)**. Under **Discovery and assessment** you should be able to see 7 discovered servers. Now click on the **Discovered servers** to view all the servers that have been discovered with the help of Azure Migrate.

    ![Screenshot of the 'Azure Migrate - Servers' blade showing 6 discovered servers under 'Azure Migrate: Server Migration'.](./Images/15-7-25-l7-1.png "Discovered servers")

1. On the **Discovered servers** page, locate the **redhat** VM in the list. We will be replicating this **redhat** VM in the next task using **Azure Migrate**.

    ![Screenshot of the 'Azure Migrate - Servers' blade showing 6 discovered servers under 'Azure Migrate: Server Migration'.](./Images/15-7-25-l7-l2.png "Discovered servers")

#### Task summary 

In this task, you get an overview of your registered Hyper-V host with the Azure Migrate Server Migration service.

### Task 2: Enable Replication from Hyper-V to Azure Migrate

In this task, you will configure and enable the replication of your on-premises virtual machine from Hyper-V to the Azure Migrate Server Migration service.

1. Return to the **Azure Migrate | Servers, databases and web apps** page and under **Migration and modernization**, select **Replicate**. This opens the **Replicate** wizard.

    ![Screenshot highlighting the 'Replicate' button in the 'Azure Migrate: Server Migration' panel of the Azure Migrate - Servers blade.](Images/15-7-25-l7-l3.png "Replicate link")
   
1. On the **Specific Intent** page, provide the following details:

    - What do you want to migrate? : Select **Servers or Virtual machines (VM)** **(1)**
    - Where do you want to migrate to? : Select **Azure VM** **(2)**
    - Are your machines virtualized? : Select **Yes, with Hyper-V (3)**
    - Click on **Continue (4)**

       ![](Images/15-7-25-l7-l4.png)

1. On the **Replicate** page, under the **Virtual machines** tab, set **Target VM security type** to **Standard or Trusted Launch Virtual machines (1)**. Under **Import migration settings from an assessment**, select **Yes, apply migration settings from an Azure Migrate assessment (2)**. Then choose **SmartHotelAssessment (3)** as the migration assessment.

    ![Screenshot of the 'Virtual machines' tab of the 'Replicate' wizard in Azure Migrate Server Migration. The Azure Migrate assessment created earlier is selected.](Images/15-7-25-l7-l5.png "Replicate - Virtual machines")

1. On the **Virtual machines** tab, you’ll now see the VMs included in the selected assessment. Select the **redhat (1)** virtual machine, then click **Next (2)**.

    ![Screenshot of the 'Virtual machines' tab of the 'Replicate' wizard in Azure Migrate Server Migration. The UbuntuWAF, smarthotelweb1, and smarthotelweb2 machines are selected.](Images/15-7-25-l7-l6.png "Replicate - Virtual machines")

1. On the **Target settings** tab, configure the following values:
   
    - Select your subscription and the existing **SmartHotelRG (1)** resource group.  
    - For **Cache storage account**, choose **migrationstorage1794187 (2)**.  
    - Under **Virtual network**, select **SmartHotelVNet (3)**.  
    - For **Subnet**, select **SmartHotel (4)**.  
    - Click **Next (5)** to continue.
 
       ![](Images/15-7-25-l7-l7.png)

       > **Note:** For simplicity, in this lab you will not configure the migrated VM for high availability, since each application tier is implemented using a single VM.

1. On the **Compute** tab, configure the following for the **redhat** virtual machine:
   
   - Select **Standard_F2s_v2** as the Azure VM size and set the **OS Type** to **Linux** **(1)**.  
   - Click **Next (2)** to proceed.

   ![](Images/15-7-25-l7-l8.png)
   
1. In the **Disks** tab, review the settings but do not make any changes. Select **Next**.

   ![](Images/15-7-25-l7-l9.png)

1. On the **Review + Start replication** tab, review the selected configuration details. Once confirmed, click **Replicate** to start the replication process.

    ![](Images/15-7-25-l7-l10.png)

1. In the **Azure Migrate | Servers, databases and web apps** page, under **Migration and modernization**, select the **Overview** button.

    ![](Images/15-7-25-l7-l11.png)
    
1. On the **Azure Migrate: Server Migration** overview page, you’ll see the **Replicate** tile under the migration dashboard. The count under **Azure VM** should show `1`, indicating that replication is in progress.

     ![](Images/15-7-25-l7-l12.png)

1. On the **Azure Migrate: Server Migration** page, select **Replications (1)** under the **Migration** section on the left. Click **Refresh (2)** occasionally and wait until the **redhat** VM shows a **Protected (3)** status. This indicates the initial replication is complete. It may take 5–10 minutes.

     ![](Images/15-7-25-l7-l13.png)

#### Task summary 

In this task, you enabled replication from the Hyper-V host to Azure Migrate and configured the replicated VM size in Azure.

## Task 3: Configure Networking

In this task, you will modify the settings for each replicated VM to use a static private IP address that matches the on-premises IP addresses for that machine.

1. Still using the **Migration and modernization - Replications** blade, select the **redhat** virtual machine. This opens a detailed migration and replication blade for this machine. Take a moment to study this information.

    ![Screenshot from the 'Azure Migrate: Server Migration - Replicating machines' blade with the smarthotelweb1 machine highlighted.](Images/infra1.11.png "Replicating machines")

2. Select **Compute and Network (1)** under **General** on the left, then select **Edit (2)**.

    ![Screenshot of the smarthotelweb1 blade with the 'Compute and Network' and 'Edit' links highlighted.](Images/upd-editcnfredhat.png "Edit Compute and Network settings")

3. Confirm that the VM is configured to use the **F2s_v2** VM size.

4. Under **Network Interfaces**, select **AzureMigrateSwitch** to open the network interface settings.

    ![Screenshot showing the link to edit the network interface settings for a replicated VM.](Images/HOL2-EX3-T3-S5.png "Network Interface settings link")

5. Change the **Private IP address** to **192.168.0.19**

    ![Screenshot showing a private IP address being configured for a replicated VM in ASR.](Images/upd-smarupdateprivate.png "Network interface - static private IP address")

6. Select **OK** to close the network interface settings blade, then **Save** the **redhat** settings to configure the private IP address for the VM.

#### Task summary 

In this task, you modified the settings for each replicated VM to use a static private IP address that matches the on-premises IP addresses for that machine

> **Note**: Azure Migrate makes a "best guess" at the VM settings, but you have full control over the settings of migrated items. In this case, setting a static private IP address ensures the virtual machine in Azure retains the same IPs they had on-premises, which avoids having to reconfigure the VM during migration (for example, by editing web.config files).

### Task 4: Server migration

In this task, you will perform a migration of the Redhat virtual machine to Azure.

> **Note**: In a real-world scenario, you would perform a test migration before the final migration. To save time, you will skip the test migration in this lab. The test migration process is very similar to the final migration.

1. Return to the **Migration and modernization** overview blade. Under **Step 3: Migrate**, select **Migrate more servers**.

    ![Screenshot of the 'Azure Migrate: Server Migration' overview blade, with the 'Migrate' button highlighted.](Images/30-09-2024(12).png "Replication summary")

1. On the **Specify Intent** blade, select **Azure VM (1)** for **Where do you want to migrate to?** and click on **Continue (2)**

    ![Screenshot of the 'Migrate' blade, with 3 machines selected and the 'Migrate' button highlighted.](Images/infra1.6.png "Migrate - VM selection")

2. On the **Migrate** blade, select **yes (1)** for **Shutdown machines before migration to minimum data loss** and select the **redhat (2)** virtual machine then select **Migrate (3)** to start the migration process.

    ![Screenshot of the 'Migrate' blade, with 3 machines selected and the 'Migrate' button highlighted.](Images/upd-starmigrationredhat.png "Migrate - VM selection")

   > **Note**: You can optionally choose whether the on-premises virtual machine should be automatically shut down before migration to minimize data loss. Either setting will work for this lab.

3. The migration process will start.

    ![Screenshot showing 3 VM migration notifications.](Images/upd-Migration3.png "Migration started notifications")

4. To monitor progress, select **Jobs (1)** under **Manage** on the left and review the status of the redhat **Planned failover (2)** job.

    ![Screenshot showing the **Jobs* link and a jobs list with 3 in-progress 'Planned failover' jobs.](Images/infra1.13.png "Migration jobs")

5. **Wait** until the **Planned failover** jobs show a **Status** of **Successful**. You should not need to refresh your browser. This could take up to 15 minutes.

    ![Screenshot showing the **Jobs* link and a jobs list with all 'Planned failover' jobs successful.](Images/infra1.14.png "Migration status")

6. Navigate to the **SmartHotelRG** resource group and check that the VM, network interface, and disk resource have been created for the Redhat virtual machine being migrated.

    ![Screenshot showing resources created by the test failover (VMs, disks, and network interfaces).](Images/upd-redhatrg.png "Migrated resources")

### Summary 

In this exercise, you reviewed the registered Hyper-V host, LabVM, with the Migration and Modernization Service, using Azure Site Recovery for migration. The Azure Site Recovery Provider was previously deployed on the Hyper-V host. You configured and enabled replication of the on-premises virtual machine to the Azure Migrate Server Migration service, adjusting settings for each replicated VM to use static private IP addresses matching their on-premises counterparts. Finally, you migrated the Red Hat virtual machine to Azure, ensuring a seamless transition to the cloud.

Click on **Next** from the lower right corner to move on to the next page.
