---
id: 31
title: 'Product: Sophos Anti-Virus &#8212; Error 1327.Invalid Drive: h:'
date: '2013-12-18T12:21:29+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=31'
permalink: /2013/12/product-sophos-anti-virus-error-1327-invalid-drive-h/
categories:
    - Registry
    - Sophos
---

Encountered this problem on my client, turns out it was caused by our domain registry redirect applying to the local Windows SYSTEM account profile as well which then meant any installations running as SYSTEM were unable to unpack correctly. Correcting all references in the following user key for SYSTEM solved the problem:

```

HKEY_USERSS-1-5-18SoftwareMicrosoftWindowsCurrentVersionExplorerUser Shell Folders
```

Equally worth looking in:

```

HKEY_LOCAL_MACHINESOFTWAREMicrosoftWindowsCurrentVersionExplorerUser Shell Folders
```