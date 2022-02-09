---
id: 1001
title: 'PowerShell get-help update-help'
date: '2019-12-11T10:46:52+00:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=1001'
permalink: /2019/12/powershell-get-help-update-help/
categories:
    - Powershell
tags:
    - error
    - get-help
    - update-help
---

Troubleshooting update-help in Powershell can be simplified using the -Force and -Ea 0 commands to continue past errors along with the to “-Ev what” to record the errors in a verbose manner to the $what variable.

The $what variable can then be reviewed more closely and the cause of the failure (hopefully) identified.

```
<pre class="wp-block-code">```
Update-Help  -Force -Ea 0 -Ev what
$what.Exception
```
```

Creds to <https://social.technet.microsoft.com/Forums/ie/en-US/0e09330a-ddb8-440e-b54c-312c99af90e4/failed-to-update-help-for-the-modules-microsoftpowershelloperationvalidation-with-ui?forum=winserverpowershell>