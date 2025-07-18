
# HOL2: Exercise 4: Optimizing newly Migrated Workloads and Emphasizing commonalities across all Stacks

### Estimated time: 40 Minutes

In this exercise, you will enable the Managed Identity feature and configure Azure Active Directory (AAD) based authentication for SSH login by deploying a VM extension on virtual machines. Additionally, you'll activate Automanage on existing machines to streamline configuration and monitoring. This process simplifies identity management and automates the operational tasks necessary for managing VMs efficiently in Azure, ensuring enhanced security and compliance across your cloud environment.

## Lab objectives

In this exercise, you will complete the following tasks:

- Task 1: Getting Started with Azure Active Directory for Linux
- Task 2: Azure Automanage

### Task 1: Getting Started with Azure Active Directory for Linux 

In this task, you will be enabling the AAD authentication using a VM extension and enabling Managed Identity. 

1. In the Azure portal `https://portal.azure.com`, navigate to your newly migrated **Red Hat** VM and select it.
    
    ![](Images/upd-redhatrg.png)
    
1. On the **redhat** virtual machine blade, expand **Security (1)** from the left-hand menu and select **Identity (2)**.

   ![](Images/15-7-25-l8-1.png)

1. In Identity, under the **System assigned** tab, turn the **Status** to **On (1)** and select **Save (2)**.
 
     > **Note**: If prompted with the Enable system-assigned managed identity pop-up, click on Yes.

     ![](Images/15-7-25-l8-2.png)

     ![](Images/15-7-25-l8-3.png)

      > **Note:** It may take a few moments to complete the process, as background operations like creating service principals are performed automatically.

      ![](Images/15-7-25-l8-4.png)
      
1. On the **redhat** virtual machine blade, expand **Settings** and select **Extensions + applications (1)** from the left-hand menu. On the **Extensions** tab, click **+ Add (2)** to install an extension that allows you to connect using your Entra ID account.
   
   ![](Images/m2e4.png)

1. On the **Install an Extension** page, search for **Azure AD based SSH Login (1)** and select it. Click **Next (2)** to proceed with the extension installation.

    ![](Images/15-7-25-l8-l1.png)

1. On the **Configure Azure AD based SSH Login Extension** page, click on **Review + create**.

    ![](Images/15-7-25-l8-7.png)

1. On the **Review + create** tab, click **Create** to start installing the extension into your Redhat VM.

    ![](Images/15-7-25-l8-8.png)

     > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
     > - Hit the Inline Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
     > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
     > - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help.

     <validation step="31b52d30-b336-49c3-a5bc-4ef69b15dd76" />

### Task 2: Azure Automanage

In this task, you will enable Automanage on existing machines.

1. In the **Azure portal**, type **Automanage (1)** in the search bar and select **Automanage (2)** from the search results.

    ![](Images/15-7-25-l4-l16.png)

1. Select **Automanage machines (1)** under **Machine best practices** and click on **+ Enable on existing machine (2)**.
   
   ![](Images/15-7-25-l8-10.png)

1. On the **Basics** tab, under **Configuration profile**, select your profile type: **Azure Best Practices - Production**.
   
   ![](Images/15-7-25-l8-11.png)
   
   > **Note:** Click View best practice profiles to see the differences between the environments.
    
   ![](Images/upd-browse-production-profile.png)

1. On the **Enable Automanage** page, select the following details.

     - Filter the list by your Subscription and Resource group and click on **Check eligibility on machines (1)**.
   
     - **Check the checkbox of the Red Hat virtual machine (2)**
   
     - Click on the **Review + Create (3)** button.
   
        ![](Images/15-7-25-l8-12.png)

1. On the **Review + Create** tab, verify the selected configuration and click **Create** to enable Automanage. Once the Configuration profile assignment is completed successfully, it will take around **5-10 minutes** to get the Status as Conformant.

    ![](Images/15-7-25-l8-13.png)

### Summary

In this exercise, you enabled Azure Active Directory (AAD) authentication and Managed Identity on virtual machines by deploying a VM extension. Additionally, you activated Automanage on existing machines to streamline configuration and monitoring. This process simplified identity management and automated the operational tasks necessary for managing VMs efficiently in Azure, ensuring enhanced security and compliance across the cloud environment.

Click on **Next** from the lower right corner to move on to the next page.

![](Images/infra-s7.png)
