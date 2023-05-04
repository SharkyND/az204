# ARM Template

Buy this
https://skillcertpro.com/product/developing-solutions-for-microsoft-azure-az-204-practice-exam-test/

Creating resource with Azure Template and Azure CLI
```
New-AzResourceGroupDeployment
-Name mydeployment -ResourceGroupName 'psdemo-rg' `
-TemplateFile './template/template.json'
-TemplateParameterFile './template/parameters.json'
```

### Intro
- The size of the virtual machine is determined by the Image
	- The image defines the combination of vCPUs, Memory and Storage Capacity
- The current limit on a per subscription basis is 20 VMs per region.
- Azure VMs are billed at an hourly rate
- A single instance VMs has an availability of 99.9% (when all storage disks are premium)
- Two instances deployed in Availability Set will give you 99.95% availability
- You can attach multiple Managed Disk to your Azure VMs

A VM is created with the following components:

![[Pasted image 20230302215318.png]]

### Sizes:

The VM are grouped with types and sizes (series / skus)

- General Purpose Balanced CPU-to-Memory ratio. Testing and development, small to medium databases, and low to medium traffic web servers. SKUs: B, Dsv3, Dv3, Dasv4, Dav4, DSv2, Dv2, Av2, DC, DCv2, Dv4, Dsv4, Ddv4, Ddsv4
- Compute Optimized High CPU-to-memory ratio. Good for medium traffic web servers, network appliances, batch processes, and app servers. SKUs: F, Fs, Fsv2
- Memory Optimized High memory-to-CPU ratio. Great for relational database servers, medium to large caches, and in-memory analytics SKUs: Esv3, Ev3, Easv4, Eav4, Ev4, Esv4, Edv4, Edsv4, Mv2, M, DSv2, Dv2
- Storage Optimized High disk throughput and IO ideal for Big Data, SQL, NoSQL databases, data warehousing and large transactional databases. SKUs: Lsv2
- GPU Specialized VMs for heavy graphic rendering and video editing, model training and inferencing (ND) with deep learning. Available with single or multiple GPUs. SKUs: NC, NCV2, NCv3, NCasT4_v3 (Preview), ND, NDv2 (Preview), NV, NVv3, NVv4
- GPU Specialized VMs for heavy graphic rendering and video editing, model training and inferencing (ND) with deep learning.Available with single or multiple GPUs. SKUs: NC, NCV2, NCv3, NCasT4_v3 (Preview), ND, NDv2 (Preview), NV, NVv3, NVv4


Azure Compute Unit (ACU) provides a way of comparing compute (CPU) performance across Azure SKUs.
ACU is currently standardized on a Small (Standard_A1) VM with the value of 100 All other SKUs then represent approximately how much faster that SKU can run a standard benchmark

![[Pasted image 20230302223953.png]]

### Connect to VM

- SSH -  PORT 22 - RSA Key Pairs
- RDP - Provides a GUI to connect to another user - PORT 3389 via  TCP and UDP
- Bastian - Lets you connect to VM using browser and azure portal

### Update Management
![[Pasted image 20230302231838.png]]

