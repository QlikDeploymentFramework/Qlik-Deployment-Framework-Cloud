# Qlik-Deployment-Framework (QDF) for Qlik Cloud (v.1.8 alfa)
These scripts are specific for Qlik Cloud, do not run under Qlik Sense desktop, QlikView or Qlik Sense server with these scripts. Qlik Cloud spaces can be used as containers as well as (and together with) classic containers stored under external storage that is  mapped as a drive in Qlik Cloud.

This is an early alfa with several bugs and limitations in Qlik Cloud. Use standard QDF containers and replace the scripts with these.  All QDF functions are loaded in during initiation but not all of functions are tested to work with Qlik Cloud.

* **An external Shared container is a must** containing these Qlik Cloud script (replacing older QDF container scripts) in an external storage. This container is need to initiate QDF using Qlik Sense reload script, using **vG.HomeContainer** as seen below:
    - `SET vG.HomeContainer='lib://user:OneDrive - user/QDF_SaaS/Shared';`
    - `$(Include=$(vG.HomeContainer)\InitLink.qvs);`
* In this release all container folders in external drives (folders you want QDF to identify as Global Variable path) need to include the **Info.txt** file, as this file identifies the folder as a Global path
* External drives are really picky on trailing slash, for OneDrive no trailing slash is possible
* To identify containers stored in external drives, the 'AltPath' to the external dirve and container root needs to be specified in `vG.SharedBaseVariablePath/ContainerMap.csv`. Do not use Excel when editing as it make the map unreadable in QDF, use an editor or DeployTool instead.
<img width="985" alt="image" src="https://github.com/QlikDeploymentFramework/Qlik-Deployment-Framework-Cloud/assets/23187088/b2f77e01-74a6-40a0-b979-d025ebd594f8">
**Qlik Cloud Space** as containers works but with limited set of folders, only global 'space' variables generated are `vG.BasePath` and `vG.QVDPath`. 
    - Mapp QDF container -> space by adding space name in `Prefix` and `ContainerName` under `vG.SharedBaseVariablePath/ContainerMap.csv` (no `AltPath` is specified)
* Use `$(include=$(vG.HomeContainer)/InitLinkSkip.qvs);` to skip executing the initiation code that identifies related containers, this only works when initiation has executed successfully one time in the same location

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
