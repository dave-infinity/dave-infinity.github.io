---
id: 1054
title: 'Ansible Notes'
date: '2021-01-05T20:31:42+00:00'
author: oxcompdave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=1054'
permalink: /2021/01/ansible-notes/
categories:
    - Ukategorisert
---

Vim indentation config

```
<pre class="wp-block-preformatted">autocmd FileType yaml setlocal ai ts=2 sw=2 et
```

```
<pre class="wp-block-preformatted" id="block-45551288-477e-4b01-919f-86f254b0ecf4">facts associated with a managed host can be obtained using the command:
```

```
<pre class="wp-block-code">```
ansible system_hostname -i inventory_file -m setup
```
```

**ansible-playbook** command with the `--ask-pass` for:

```
<pre class="wp-block-code">```
- name: Public key is deployed to managed hosts for Ansible
  hosts: all

  tasks:
    - name: Ensure key is in root's ~/.ssh/authorized_hosts
      authorized_key:
        user: root
        state: present
        key: '{{ item }}'
      with_file:
        - ~/.ssh/id_rsa.pub
```
```