# Qlik-Deployment-Framework (QDF)
**QDF version 1.8**
Version for Qlik Cloud
This is an early alfa with several bugs and limitations in Qlik Cloud. 
* Shared container is a must and need to be mapped within the reload script, as seen below:
    SET vG.SharedBasePath='lib://Drive name/path/Shared';
    $(include=$(vG.SharedBasePath)/InitLink.qvs);
* In this release all container folders in external drives (folders you want to QDF to identify as Global Variable path) need to include the Info.txt file, as this file identifies the folder as a Global path
* external drives are really picky on trailing slash, for OneDrive no trailing slash is possible
* To identify containers stored in external drives, the base URL need to be specified in vG.SharedBaseVariablePath/ContainerMap.csv
* To identify spaces as containers just add the space name under vG.SharedBaseVariablePath/ContainerMap.csv
* Qlik Cloud spaces has limited support for subfolders, so adding QDF containers to spaces (by same name) only vG.BasePath and vG.QVDPath will work

## QDF is a set of Qlik scripts and utilities that enables: 
Resource Sharing, Reuse, Organization, Structure and Standards providing an effective and efficient Qlik deployment.
Qlik-Deployment-Framework content is available at https://community.qlik.com/groups/qlikview-deployment-framework

## Qlik Deployment Framework resource containers
QDF is based on a resource container architecture. Arrange containers (building blocks and security separators) to fit the current needs, when demand changes its easy to reorganize and add additional containers. QlikView and/or Qlik Sense applications are hooked into the containers in which all needed resources reside.

## Qlik Deployment Framework Deploy Tool binary releases
Available under releases tab: https://github.com/QlikDeploymentFramework/Qlik-Deployment-Framework/releases

## Qlik-Deployment-Framework GitHub repository
Qlik-Deployment-Framework GitHub repository contains Qlik Script code that resides inside each QDF container, not the complete container.
## Qlik-Deployment-Framework GitHub content:
- **Version1.7.5.txt** --> File containing version number and code modifications
- **InitLink.qvs** --> Initiation script that links Qlik Sense/QlikView to 1.Init.qvs
- **InitLinkSkip.qvs** -->  InitLinkSkip.qvs removes script complexity and there by making debugging easier during developing
- **3.Include/1.BaseVariable/1.Init.qvs** --> Main initiation script for both Qlik Sense and QlikView (run automatically by InitLink.qvs) 1.Init.qvs will validate and create global variables for the current environment.
- **3.Include/1.BaseVariable/3.SystemVariables.qvs** --> Only for QlikView, loads system variables (filepath to logs and more)
- **3.Include/2.Locale** --> contains locale files used during initiation
- **3.Include/4.Sub**  --> contains the most important function library, read more under README https://github.com/QlikDeploymentFramework/Qlik-Deployment-Framework/tree/master/3.Include/4.Sub

