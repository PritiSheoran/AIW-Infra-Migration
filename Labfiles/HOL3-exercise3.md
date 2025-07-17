
# HOL3: Exercise 3: Setup Test Failover


### Estimated time: 25 Minutes

In this exercise, you will deploy a Test Failover to the replicated Virtual Machine, which allows you to test the sanity of the virtualized workload without interrupting your production workload or ongoing replication.

## Lab objectives

In this exercise, you will complete the following task:

- Task 1: Setup Test Failover

### Task 1: Setup Test Failover

1. On the **Recovery Service Vault page**, expand the **Protected Items (1)** and click on **Replicated Items (2)** and select **AzureArcVM (3)** that you replicated in the previous exercise.
   
    ![](Images/15-7-25-l11-1.png) 
   
1. On the **AzureArcVM** page, click on **Test Failover**.  

    ![](Images/15-7-25-l11-2.png) 
   
1. On the **Test failover** page, select **SmartHotelVNet (1)** under Azure virtual network and click **OK (2)** to initiate the test failover.

    ![Screenshot of the Test Failover page.](Images/hol3-e3-s4.png "Test Failover page") 
    
1. Go back to the **Replicated items** page. Under **Monitoring (1)** in the left-hand panel, select **Site Recovery jobs (2)** and then click on **Test failover (3)** to view the job status.

    ![](Images/15-7-25-l11-3-new.png) 

1.  On the **Test failover** job details page, wait for **10–15 minutes** for the **Test failover** job to complete successfully and reflect the **Successful** status across key steps in the job list.
   
    ![](Images/15-7-25-l11-4.png) 
  
1. In the **Search resources, services, and docs** bar, type **Virtual Machines** **(1)** and select **Virtual machines** from the Services **(2)**.

   ![](Images/15-7-25-l11-4.1.png) 

1. On the **Virtual machines** page, select **AzureArcVM-test** which is automatically created after the test failover.

   ![](Images/15-7-25-l11-5.png) 
  
1. On the **AzureArcVM-test page**, verify that the status of the VM is in **Running state (1)** and click on **Connect (2).** Then select the **Native RDP** option and connect to the VM through RDP.    

    ![Screenshot of the Test vm status.](Images/HOL3E3S8.png "Test vm status") 

### Summary 

In this exercise, you learnt how to validate the replication and disaster recovery strategy by testing a failover, that too without any data loss or downtime.

Click on **Next** from the lower right corner to move on to the next page.

![](Images/14-next.png) 
