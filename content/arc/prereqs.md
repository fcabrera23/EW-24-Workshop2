---
section_id: Arc
nav_order: 3
title: Arc Prerequisites
---

This section provides Azure CLI commands that you can run with an Azure subscription. If you don't have an Azure subscription already, create one for free now.

| ℹ️ Note                                   | 
|------------------------------------------|
| _You need an Azure subscription with either the Owner role or a combination of Contributor and User Access Administrator roles. You can check your access level by navigating to your subscription on the Azure portal, selecting Access control (IAM) on the left-hand side of the Azure portal, and then selecting View my access. For more information, see how to manage Azure resource groups by using the Azure portal._ | 
| | 

### Instructions

1. Set up the Azure subscription - Using local `az cli` or  **Azure Cloud Shell**, run the following command. Replace the value of <your-Azure-subscription-ID> with your Azure subscription ID value:

    ```bash
    subscriptionid="<your-Azure-subscription-ID>
    az account set --subscription $subscriptionid
    ```

2. Create a new Resourge Group

    ```bash
    resourcegroup="aksedge-training"
    location="westus3"
    az group create --name $resourcegroup --location $location
    ```

3. Create a new Service Principal with the built-in **Owner** role and restricted to the resource group scope. This service principal is used to connect to Azure Arc. Use the `az ad sp create-for-rbac` command:

    ```bash
    resourcegroup="aksedge-training"
    serviceprincipalname="aksedge-sp"
    subscriptionid=$(az account show --query id -o tsv)
    az ad sp create-for-rbac --name $serviceprincipalname --role "Owner" --scopes /subscriptions/$subscriptionid/resourceGroups/$resourcegroup
    ```

    | ℹ️ Note                                   | 
    |------------------------------------------|
    | _Take a note of the Service Principal appId and Service Principal password. You will need it later._ | 
    | | 

4. Enable all required resource providers in the Azure subscription using the az provider register command:

    ```bash
    az provider register --namespace Microsoft.HybridCompute
    az provider register --namespace Microsoft.GuestConfiguration
    az provider register --namespace Microsoft.HybridConnectivity
    az provider register --namespace Microsoft.Kubernetes
    az provider register --namespace Microsoft.KubernetesConfiguration
    az provider register --namespace Microsoft.ExtendedLocation
    ```