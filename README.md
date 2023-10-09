# Qlik-Deployment-Framework (QDF) for Qlik Cloud (v.1.8 beta)
These scripts are specific for Qlik Cloud, do not run under Qlik Sense desktop, QlikView or Qlik Sense server with these scripts. Qlik Cloud spaces can be used as containers as well as (and together with) classic containers stored under external storage that is  mapped as a drive in Qlik Cloud.

This is now in beta. Initiation (InitLink.qvs) has been tested and validated. Sub functions has been adapted for Qlik Cloud. Still lacking testing and validation from community

* Use standard QDF containers and replace the sub functions and initiation scripts with Qlik-Deployment-Framework-Cloud
* All the updated Qlik-Deployment-Framework-Cloud functions are loaded in during initiation (InitLink.qvs)

* **An external Shared container is a must** containing these Qlik Cloud script (replacing older QDF container scripts) in an external storage. This container is need to initiate QDF using Qlik Sense reload script, using **vG.HomeContainer** as seen below:
    - `SET vG.HomeContainer='lib://user:OneDrive - user/QDF_SaaS/Shared';`
    - `$(Include=$(vG.HomeContainer)\InitLink.qvs);`
* In this release all container folders in external drives (folders you want QDF to identify as Global Variable path) need to include the **Info.txt** file, as this file identifies the folder as a Global path
* Use `$(include=$(vG.HomeContainer)/InitLinkSkip.qvs);` to skip executing the initiation code that identifies related containers, this only works when initiation has executed successfully one time in the same location
* External drives are really picky on trailing slash, for OneDrive no trailing slash is possible
* To identify containers stored in external drives. Edit the shared `vG.SharedBaseVariablePath/ContainerMap.csv`add the external storage location, inlcuding container root in `AltPath` field as a URL, as seen below. Remember that its the URL to `QDF starting folder`, not the container itself (as the container name already exists under `ContainerName` field). Do not use Excel when editing as it make the map unreadable in QDF, use an editor or DeployTool instead.
<img width="985" alt="image" src="https://github.com/QlikDeploymentFramework/Qlik-Deployment-Framework-Cloud/assets/23187088/b2f77e01-74a6-40a0-b979-d025ebd594f8">

## Assign containers to Qlik Cloud Spaces
Its possible to use Spaces as containers but with limited set of folders, only global variables generated for a space are `vG.BasePath` and `vG.QVDPath`. 
    - Assign space as QDF container by typing space name under `Prefix` and `ContainerName` in shared container map `vG.SharedBaseVariablePath/ContainerMap.csv`. Leave `AltPath` empty as this is reserved for external storage location

## Containers without number and devider
To be compatible with Sharepoint storage its now possible to use container folders that does not contain number and devider (like 1.). Just take a standard container and remove numbers and deviders on all  subfolders, QDF initiation should identify and resolve folders as GlobalVariables anyhow.

<img width="150" alt="image" src="https://github.com/QlikDeploymentFramework/Qlik-Deployment-Framework-Cloud/assets/23187088/825ac094-c122-4ba5-a191-c7e2a342e304">

## QDF is a set of Qlik scripts and utilities that enables: 
Resource Sharing, Reuse, Organisation, Structure and Standards providing an effective and efficient Qlik deployment.
Qlik-Deployment-Framework content is available at https://community.qlik.com/groups/qlikview-deployment-framework

## Qlik Deployment Framework resource containers
QDF is based on a resource container architecture. Arrange containers (building blocks and security separators) to fit the current needs, when demand changes its easy to reorganize and add additional containers. QlikView and/or Qlik Sense applications are hooked into the containers in which all needed resources reside.

## Qlik Deployment Framework Deploy Tool binary releases
Available under releases tab: https://github.com/QlikDeploymentFramework/Qlik-Deployment-Framework/releases

## Qlik-Deployment-Framework GitHub repository
Qlik-Deployment-Framework GitHub repository contains Qlik Script code that resides inside each QDF container, not the complete container.
## Qlik-Deployment-Framework GitHub content:
- **Version1.8.txt** --> File containing version number and code modifications
- **InitLink.qvs** --> Initiation script that initiates the framework and links to 1.Init.qvs
- **InitLinkSkip.qvs** -->  InitLinkSkip.qvs removes script complexity and there by making debugging easier during developing
- **Info.txt** --> Info file that describes the folders purpose and is used to identify that this folder should be mapped to a GlobalVariable
- **3.Include/1.BaseVariable/1.Init.qvs** --> Main initiation script for both Qlik Sense and QlikView (run automatically by InitLink.qvs) 1.Init.qvs will validate and create global variables for the current environment and load all functions and potential custom variables.
- **3.Include/1.BaseVariable/ContainerMap.csv** --> Contains a list of the containers identified by QDF, this list need to be up to date for QDF to work properly. Qlik Cloud spaces can be used as containers as well as real containers stored under external storage that is  mapped as a drive in Qlik Cloud
- **3.Include/2.Locale** --> contains locale files used during initiation
- **3.Include/4.Sub**  --> contains the most important function library, read more under README https://github.com/QlikDeploymentFramework/Qlik-Deployment-Framework/tree/master/3.Include/4.Sub
