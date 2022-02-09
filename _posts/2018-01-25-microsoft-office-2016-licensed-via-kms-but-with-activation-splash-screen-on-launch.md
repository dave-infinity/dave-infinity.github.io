---
id: 825
title: 'Microsoft Office 2016 Licensed via KMS but with Activation Splash Screen on launch'
date: '2018-01-25T13:37:35+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=825'
permalink: /2018/01/microsoft-office-2016-licensed-via-kms-but-with-activation-splash-screen-on-launch/
categories:
    - Microsoft
tags:
    - '2016'
    - 'ms office'
    - office
---

Resolved by following https://support.office.com/en-us/article/Office-repeatedly-prompts-you-to-activate-on-a-new-PC-a9a6b05f-f6ce-4d1f-8d49-eb5007b64ba1

- Close the activation window and all Office apps.
- Right-click the **Start** button ![Windows Start button in Windows 8 and Windows 10](https://support.content.office.net/en-us/media/de9c1ffe-f29a-47b1-a811-95ca547d07c6.png "Windows Start button in Windows 8 and Windows 10") on the lower-left corner of your screen, and select **Run**.
- Type **regedit**, and then press **Enter**. Select **Yes** when prompted to open the Registry Editor.
- On the left side of the Registry Editor, under **Computer**, navigate to the following key in the registry: **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\Office\\16.0\\Common\\OEM**
- Right click the **OEM** value and click **File&gt;Export**.
- Save the key.
- After the key is backed up, select **Edit&gt;Delete**.
- Repeat steps 3-6 for the following key: **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Office\\16.0\\Common\\OEM**
- Close the Registry Editor and start Office again.