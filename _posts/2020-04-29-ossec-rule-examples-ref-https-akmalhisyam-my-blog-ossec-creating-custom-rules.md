---
id: 1020
title: 'OSSEC Rule Examples'
date: '2020-04-29T14:32:48+01:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=1020'
permalink: /2020/04/ossec-rule-examples-ref-https-akmalhisyam-my-blog-ossec-creating-custom-rules/
categories:
    - Linux
    - Software
---

## Direct copy from the blog [https://akmalhisyam.my/blog/ossec-creating-custom-rules ](https://akmalhisyam.my/blog/ossec-creating-custom-rules)for my reference – thanks Akmal!

When parsing log, OSSEC will look at level 0 first, and then highest level -&gt; lowest levelOSSEC will not produce alert for rules with level 0It is best to put custom rules in local\_rules.xml or other file to avoid being overwritten during upgradeossec-logtest is a very useful tool to test your rules &amp; decoder

## Example

#### Silencing certain rules

```
<pre class="wp-block-code">```
<rule id="100030" level="0">
  <if_sid>503,502</if_sid>
  <description>List of rules to be ignored.</description>
</rule>
```
```

OSSEC will not produce any alert when rule 502 and 503 is triggered

- - - - - -

#### Ignore alert if rules triggered by certain IP

```
<pre class="wp-block-code">```
<rule id="100225" level="0">
  <if_sid>40101</if_sid>
  <srcip>127.0.0.1</srcip>
  <description>Ignore this</description>
</rule>
```
```

If rule 40101 triggered by 127.0.0.1, dont produce any alert

- - - - - -

#### Ignore alert if contains certain strings

```
<pre class="wp-block-code">```
<rule id="100223" level="0">
  <if_sid>1002</if_sid>
  <match>terrorist|terror|femmefatale|heart-attack</match>
  <description>Ignore 1002 false positive</description>
</rule>
```
```

OSSEC is using [OS\_match/sregex](https://ossec-docs.readthedocs.io/en/latest/syntax/regex.html) syntax in &lt;match&gt;

- - - - - -

#### Ignore alert if contains certain strings (using regex)

```
<pre class="wp-block-code">```
<rule id="100207" level="4">
  <if_sid>1002,1003</if_sid>
  <regex>^WordPress database error You have an error in your SQL syntax(\.*)functionName$</regex>
  <description>Unescaped SQL query, known issue</description>
</rule>
```
```

OSSEC is using [OS\_regex/regex](https://ossec-docs.readthedocs.io/en/latest/syntax/regex.html) syntax in &lt;regex&gt;

- - - - - -

#### Trigger custom rule when certain field match certain value in cdb list

```
<pre class="wp-block-code">```
<rule id="100215" level="5">
  <if_sid>31101</if_sid>
  <list lookup="match_key" field="url">rules/badurl</list>
  <description>URL is in badurl</description>
</rule>
```
```

- - - - - -

#### Trigger custom rule when certain rules is fired x time within n second from same srcip

```
<pre class="wp-block-code">```
<rule id="100216" level="10" frequency="4" timeframe="90">
  <if_matched_sid>100215</if_matched_sid>
  <same_source_ip />
  <description>Multiple badurl access </description>
  <description>from same source ip.</description>
  <group>web_scan,recon,</group>
</rule>
```
```

- - - - - -

#### Overriding rules

```
<pre class="wp-block-code">```
<rule id="1003" level="13" overwrite="yes" maxsize="2000">
  <description>Non standard syslog message (size too large).</description>
</rule>
```
```

Original rule 1003 have 10245 as its maxsize. Using overwrite=”yes” will make OSSEC overwrite certain field in original rule

- - - - - -

#### Custom rule group

```
<pre class="wp-block-code">```
<group name="app_error">
  <rule id="100207" level="4">
    <if_sid>1002,1003</if_sid>
    <regex>^WordPress database error You have an error in your SQL syntax(\.*)functionName$</regex>
    <description>Unescaped SQL query, known issue</description>
  </rule>

  <rule id="100218" level="0">
    <if_sid>1003</if_sid>
    <match>WUID | WTB</match>
    <description>ignorance is bliss</description>
  </rule>
</group>
```
```