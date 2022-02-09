---
id: 95
title: 'msiexec error codes'
date: '2014-01-27T09:31:11+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=95'
permalink: /2014/01/msiexec-error-codes/
categories:
    - 'error codes'
    - Microsoft
    - Windows
---

taken from [http://www.msierrors.com/tag/1618/](http://www.msierrors.com/tag/1618/ "http://www.msierrors.com/tag/1618/")

\[expand title=”msiexec codes”\]

| ###### VALUE RETURNED | ###### ERROR CODE | ###### ERROR DESCRIPTION | ###### SOLUTION |
|---|---|---|---|
| ###### 0 | ###### ERROR\_SUCCESS | ###### Action completed successfully. | ###### Nothing to be done |
| ###### 13 | ###### ERROR\_INVALID\_DATA | ###### The data is invalid |
| ###### 87 | ###### ERROR\_INVALID\_PARAMETER | ###### One of the parameters was invalid. |
| ###### **1601** | ###### ERROR\_INSTALL\_SERVICE\_FAILURE | ###### The Windows Installer service could not be accessed. Contact your support personnel to verify that the Windows Installer service is properly registered. | ###### There’s a problem with the Windows Installer Service. It might happen after a KB that affects it has just been installed. Solution: Restarting the machine usually solves the problem. |
| ###### 1602 | ###### ERROR\_INSTALL\_USEREXIT | ###### User cancel installation. | ###### The user has cancelled the installation. Solution: just don’t cancel it |
| ###### **1603** | ###### ERROR\_INSTALL\_FAILURE | ###### Fatal error during installation. | ###### It’s the most common error code. It means something is wrong with the package. |
| ###### 1604 | ###### ERROR\_INSTALL\_SUSPEND | ###### Installation suspended, incomplete. |
| ###### **1605** | ###### ERROR\_UNKNOWN\_PRODUCT | ###### This action is only valid for products that are currently installed. | ###### This happens when you try to uninstall/repair an MSI using its product code. Solution: Check if the product is installed first. For example, the existance of HKCRInstallerProductshash corresponding key |
| ###### 1606 | ###### ERROR\_UNKNOWN\_FEATURE | ###### Feature ID not registered. |
| ###### 1607 | ###### ERROR\_UNKNOWN\_COMPONENT | ###### Component ID not registered. |
| ###### 1608 | ###### ERROR\_UNKNOWN\_PROPERTY | ###### Unknown property. |
| ###### 1609 | ###### ERROR\_INVALID\_HANDLE\_STATE | ###### Handle is in an invalid state. |
| ###### 1610 | ###### ERROR\_BAD\_CONFIGURATION | ###### The configuration data for this product is corrupted. Contact your support personnel. |
| ###### 1611 | ###### ERROR\_INDEX\_ABSENT | ###### Component qualifier not present. |
| ###### 1612 | ###### ERROR\_INSTALL\_SOURCE\_ABSENT | ###### The installation source for this product is not available. Verify that the source exists and that you can access it. |
| ###### 1613 | ###### ERROR\_INSTALL\_PACKAGE\_VERSION | ###### This installation package cannot be installed by the Windows Installer service. You must install a Windows service pack that contains a newer version of the Windows Installer service. |
| ###### 1614 | ###### ERROR\_PRODUCT\_UNINSTALLED | ###### Product is uninstalled. |
| ###### 1615 | ###### ERROR\_BAD\_QUERY\_SYNTAX | ###### SQL query syntax invalid or unsupported. |
| ###### 1616 | ###### ERROR\_INVALID\_FIELD | ###### Record field does not exist. |
| ###### **1618** | ###### ERROR\_INSTALL\_ALREADY\_RUNNING | ###### Another installation is already in progress. Complete that installation before proceeding with this install. | ###### This happens when you try to install a product while another installation is in progress. Solution: Wait until the previous installation is finished. |
| ###### **1619** | ###### ERROR\_INSTALL\_PACKAGE\_OPEN\_FAILED | ###### This installation package could not be opened. Verify that the package exists and that you can access it, or contact the application vendor to verify that this is a valid Windows Installer package. | ###### Either the file (MSI) doesn’t exist, or it’s being locked for editing (by tools such as Orca, insted, etc). Solution: Check the location and make sure no process holds it locked. |
| ###### 1620 | ###### ERROR\_INSTALL\_PACKAGE\_INVALID | ###### This installation package could not be opened. Contact the application vendor to verify that this is a valid Windows Installer package. |
| ###### 1621 | ###### ERROR\_INSTALL\_UI\_FAILURE | ###### There was an error starting the Windows Installer service user interface. Contact your support personnel. |
| ###### 1622 | ###### ERROR\_INSTALL\_LOG\_FAILURE | ###### Error opening installation log file. Verify that the specified log file location exists and is writable. | ###### Solution: Make sure you have the permissions to write to the log file. Or change its location. |
| ###### 1623 | ###### ERROR\_INSTALL\_LANGUAGE\_UNSUPPORTED | ###### This language of this installation package is not supported by your system. |
| ###### **1624** | ###### ERROR\_INSTALL\_TRANSFORM\_FAILURE | ###### Error applying transforms. Verify that the specified transform paths are valid. | ###### Solution: Make sure the path to the MST is correct. |
| ###### 1625 | ###### ERROR\_INSTALL\_PACKAGE\_REJECTED | ###### This installation is forbidden by system policy. Contact your system administrator. |
| ###### 1626 | ###### ERROR\_FUNCTION\_NOT\_CALLED | ###### Function could not be executed. |
| ###### 1627 | ###### ERROR\_FUNCTION\_FAILED | ###### Function failed during execution. |
| ###### 1628 | ###### ERROR\_INVALID\_TABLE | ###### Invalid or unknown table specified. |
| ###### 1629 | ###### ERROR\_DATATYPE\_MISMATCH | ###### Data supplied is of wrong type. |
| ###### 1630 | ###### ERROR\_UNSUPPORTED\_TYPE | ###### Data of this type is not supported. |
| ###### 1631 | ###### ERROR\_CREATE\_FAILED | ###### The Windows Installer service failed to start. Contact your support personnel. |
| ###### 1632 | ###### ERROR\_INSTALL\_TEMP\_UNWRITABLE | ###### The temp folder is either full or inaccessible. Verify that the temp folder exists and that you can write to it. |
| ###### 1633 | ###### ERROR\_INSTALL\_PLATFORM\_UNSUPPORTED | ###### This installation package is not supported on this platform. Contact your application vendor. |
| ###### 1634 | ###### ERROR\_INSTALL\_NOTUSED | ###### Component not used on this computer. |
| ###### 1635 | ###### ERROR\_PATCH\_PACKAGE\_OPEN\_FAILED | ###### This patch package could not be opened. Verify that the patch package exists and that you can access it, or contact the application vendor to verify that this is a valid Windows Installer patch package. |
| ###### 1636 | ###### ERROR\_PATCH\_PACKAGE\_INVALID | ###### This patch package could not be opened. Contact the application vendor to verify that this is a valid Windows Installer patch package. |
| ###### 1637 | ###### ERROR\_PATCH\_PACKAGE\_UNSUPPORTED | ###### This patch package cannot be processed by the Windows Installer service. You must install a Windows service pack that contains a newer version of the Windows Installer service. |
| ###### 1638 | ###### ERROR\_PRODUCT\_VERSION | ###### Another version of this product is already installed. Installation of this version cannot continue. To configure or remove the existing version of this product, use Add/Remove Programs in Control Panel. |
| ###### 1639 | ###### ERROR\_INVALID\_COMMAND\_LINE | ###### Invalid command line argument. Consult the Windows Installer SDK for detailed command line help. |
| ###### 1640 | ###### ERROR\_INSTALL\_REMOTE\_DISALLOWED | ###### Installation from a Terminal Server client session not permitted for current user. |
| ###### 1641 | ###### ERROR\_SUCCESS\_REBOOT\_INITIATED | ###### The installer has started a reboot. |
| ###### 1642 | ###### ERROR\_PATCH\_TARGET\_NOT\_FOUND | ###### The installer cannot install the upgrade patch because the program being upgraded may be missing, or the upgrade patch updates a different version of the program. Verify that the program to be upgraded exists on your computer and that you have the correct upgrade patch. |
| ###### **3010** | ###### ERROR\_SUCCESS\_REBOOT\_REQUIRED | ###### A restart is required to complete the install. This does not include installs where the ForceReboot action is run. |

\[/expand\]