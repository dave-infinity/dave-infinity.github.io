---
id: 950
title: 'Powershell Domain Controller Assessment'
date: '2019-08-09T08:32:03+01:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=950'
permalink: /2019/08/powershell-domain-controller-assessment/
categories:
    - Microsoft
    - Powershell
---

To get a list of the FSMO Role holders for a Single Domain.

<figure class="wp-block-table">| 1 | Get-ADDomain \| Select-Object DistinguishedName, SchemaMaster, DomainNamingMaster, InfrastructureMaster, PDCEmulator, RIDMaster |
|---|---|

</figure>To get a list of the FSMO Role holders in a Forest.

<figure class="wp-block-table">| 1 | Get-ADForest \| Select-Object Name,SchemaMaster, DomainNamingMaster,InfrastructureMaster, PDCEmulator, RIDMasterall |
|---|---|

</figure>To get a nicely formatted list with all the Domain Controllers and who owns which particular role.

<figure class="wp-block-table">| 1 | Get-ADDomainController -Filter \* \| Select-Object Name, Domain, Forest, OperationMasterRoles \| Where-Object {$\_.OperationMasterRoles} |
|---|---|

</figure>ref: https://www.markou.me/2016/10/get-list-fsmo-role-holders-using-powershell-one-liners/