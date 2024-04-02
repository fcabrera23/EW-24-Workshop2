---
section: AIO
title: Edge Storage Accelerator
nav_order: 5
---

Edge Storage Accelerator (ESA) is a Microsoft 1P storage system designed for Arc-connected Kubernetes clusters. ESA can be deployed to write files to a **ReadWriteMany** persistent volume claim (PVC) where they are then shuttled up to Azure Blob Storage. It offers a range of features to support Azure IoT Operations and other Arc Services. 

Edge Storage Accelerator (ESA) serves as a native persistent storage system for Arc-connected Kubernetes clusters. Its primary role is to provide a reliable, fault-tolerant file system that allows data to be tiered to Azure. For Azure IoT Operations (AIO) and other Arc Services, ESA is crucial in making Kubernetes clusters stateful

### Instructions

1. Install Open Service Mesh (OSM)
    ```powershell
    az k8s-extension create --resource-group "YOUR_RESOURCE_GROUP_NAME" --cluster-name "YOUR_CLUSTER_NAME" --cluster-type connectedClusters --extension-type Microsoft.openservicemesh --scope cluster --name osm
    ```

1. Install the Edge Storage Accelerator Arc Extension
    ```powershell
    az k8s-extension create --resource-group "${YOUR-RESOURCE-GROUP}" --cluster-name "${YOUR-CLUSTER-NAME}" --cluster-type connectedClusters --name hydraext --extension-type microsoft.edgestorageaccelerator
    ```
    
1. 