---
section: AKS-EE
title: Deploy and Arc-connect AKS-EE cluster
---

In this module, you will:

- Create a new AKS-EE cluster with the required Azure IoT Operations (AIO) configurations
- Connect the cluster to Arc


### Instructions

1. Open an elevated PowerShell window, change the directory to a working folder, then run the following commands:

    ```powershell
    $url = "https://raw.githubusercontent.com/Azure/AKS-Edge/main/tools/scripts/AksEdgeQuickStart/AksEdgeQuickStartForAio.ps1"
    Invoke-WebRequest -Uri $url -OutFile .\AksEdgeQuickStartForAio.ps1
    Unblock-File .\AksEdgeQuickStartForAio.ps1
    Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process -Force
    ```

    This script automates the following steps:

    * Download the GitHub archive of Azure/AKS-Edge into the working folder and unzip it to a folder AKS-Edge-main (_or AKS-Edge-\<tag>_). By default, the script downloads the **main** branch.

    * Validate that the correct az cli version is installed and ensure that az cli is logged into Azure.

    * Download and install the AKS Edge Essentials MSI.

    * Install required host OS features (Install-AksEdgeHostFeatures).

    * Deploy a single machine cluster with internal switch (Linux node only).

    * Create the Azure resource group in your Azure subscription to store all the resources.

    * Connect the cluster to Azure Arc and registers the required Azure resource providers.

    * Apply all the required configurations for Azure IoT Operations, including:

    * Enable a firewall rule and port forwarding for port 8883 to enable incoming connections to Azure IoT Operations  broker.

    * Install Storage local-path provisioner.

    * Enable node level metrics to be picked up by Azure Managed Prometheus.

1. In an elevated PowerShell prompt, run the `AksEdgeQuickStartForAio.ps1` script. This script brings up a K3s cluster. Replace the placeholder parameters with your own information.

    ```powerShell
   .\AksEdgeQuickStartForAio.ps1 -SubscriptionId "<SUBSCRIPTION_ID>" -TenantId "<TENANT_ID>" -ResourceGroupName "<RESOURCE_GROUP_NAME>"  -Location "<LOCATION>"  -ClusterName "<CLUSTER_NAME>"
   ```

   | Placeholder | Value |
   | ----------- | ----- |
   | `SUBSCRIPTION_ID` | ID of the subscription where your resource group and Arc-enabled cluster will be created. |
   | `TENANT_ID` | ID of your Microsoft Entra tenant. |
   | `RESOURCE_GROUP_NAME` | A name for a new resource group. |
   | `LOCATION` | An Azure region close to you. The following regions are supported in public preview: East US2, West US 3, West Europe, East US, West US, West US 2, North Europe. |
   | `CLUSTER_NAME` | A name for the new connected cluster. |
   | |  | 

    When the script is completed, it brings up an Arc-enabled K3s cluster on your machine.

1. Run the following commands to check that the deployment was successful:

    ```powershell
    Import-Module AksEdge
    Get-AksEdgeDeploymentInfo
    ```
