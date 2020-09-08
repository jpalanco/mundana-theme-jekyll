---
title: "The Right Way to Publish a CVE"
date: "2020-8-9"
image: assets/images/cve.jpeg
author: name
layout: post
tags: [ publish, CVE ]
categories: [ CVE ]
---

The Right Way to Publish a CVE

## What Is a CVE?

A CVE is a dictionary of publicly known cybersecurity vulnerabilities which is intended to uniquely identify and name publicly disclosed vulnerabilities pretraining to specific versions of a software or a codebase.

Stakeholders have confidence that they can refer to a CVE identifier or ID and know that they are talking about a specific and unique venerability regardless of the tool or form which is used.

In other words, a CVE is the standard for uniquely identifying vulnerabilities, and a dictionary of publicly known cybersecurity vulnerabilities.

It can also be seen as a pivot point between vulnerability scanners, vendor patch information, and cyber operations as a whole.

A CVE is not a vulnerability mitigation, database or a source for vulnerability risks, impacts, fixes or technical information.

It is also not a tool for publicly disclosing vulnerabilities.

The MITRE Corporation can oversee the CVE program operationally and administratively, while CNAs are organizations that assign CVE IDs to researchers and vendors for inclusion in the first-time public announcements of new vulnerabilities which have been discovered.

Each CAN has a specific scope of responsibility, delimiting what products, informational sources or domains for which they can assign CVEs.

## When Can a CVE ID Request Be Made?

When you have identified a new, or previously unassigned vulnerability in any product.

You do not however have to be the one who discovered it.

If you have attempted to contact the vendor or developer of the affected product, and the vendor or developer is a CAN, they will assign the CVE id for you.

If the vendor or developer is not a CAN, they need to verify if the issue is reported or if another CVE id has already been assigned or the issue.

Keep in mind that the vulnerability does not need to be public before a request for a CVE ID is made, but it does need to be public to be included to the CVE list as a whole.

Counting is a method used by CVE to determine I a bug has vulnerabilities, or if a vulnerability is already found, how many of them are within the software.

The Counting process summary goes as followed:  
You need to start by breaking the report into a few individual bugs.

Determine if the individual bugs result in vulnerabilities.

If you discover that they result in vulnerabilities, you need to analyze how many of them are there, and if they warrant a CVE ID.

If you discover that the bugs do not have any vulnerabilities, determine if a different combination of the bugs result in one.

The information about the vulnerability must be public and the community must be able to do something to mitigate it.

The community has to be concerned about the security of the product, and finally, you need to determine if a CVE ID has already been assigned to the vulnerability.

If it has not, you can make a request.

## How to make a Request for a CVE ID

To do this, start by visiting https://cveform.mitre.org/ and clicking on ”Request a CVE ID”.

You will need to provide the following information:  
Vulnerability type, vendor or developer o the product, the affected product and version information, and in some cases, you might also need to mention the attack type, the impact, the affected component, the attack vector, information about how the vendor acknowledged the vulnerability and some public references.

Once the request is submitted, you will be greeted by a confirmation email message.

MITRE will review the request.

<![if !supportLists]>· <![endif]>If there is sufficient information which indicates that the assignment is in fact, valid, then the Content Team will send you the CVE ID that you can use.

<![if !supportLists]>· <![endif]>If the vulnerability is a product covered by a CAN, you will be directed to the appropriate CAN.

<![if !supportLists]>· <![endif]>If there is not enough information to indicate that it is valid, you will be asked for more information.

If a CVE ID is assigned to the vulnerability, it will be marked as “RESERVED” in the list.

The CVE ID entry does not contain any vulnerability details during this phase.

To publish these, a CVE ID must reference public information.

Public references simply have to be included in a CVE ID before publication.

Once the CVE ID has a public reference, and MITRE or the CAN has been notified that it is public, MITRE will populate the CVE entry description and publish it.

## The Proper Way to Write a Description

In this description, you have to write the product, the version, and the problem type information.

They are submitted in a separate field, and they need to be in both locations because the separate fields are not included in the CVE list used by downstream users.

The CVE program has to be trusted not to leak the privileged information reporters share with it, and this requires that each and every detail is backed up by another source which helps with this.

Only relevant information about the vulnerability needs to be included, and it must be written in the English language when it is sent to the Primary CAN.

MITRE has their own description format which looks something like this:

<![if !supportLists]>· <![endif]>[VULNTYPE] in [COMPONENT] in [VENDOR][PRODUCT] [VERSION] allows [ATTACKER] to [IMPACT] via [VECTOR].

<![if !supportLists]>· <![endif]>[COMPONENT] in [VENDOR] [PRODUCT]  [VERSION] [ROOT CAUSE], which allows  [ATTACKER] to [IMPACT] via [VECTOR].

You can find additional information about the MITRE style here:

[https://cveproject.github.io/docs/content/key-details-phrasing.pdf](https://cveproject.github.io/docs/content/key-details-phrasing.pdf)

To update an existing CVE ID, you need to have additional information to add to a CVE entry.

This way, you can request that the entry is updated with this additional information, and you can update it with references, descriptions, or in some cases, eve dispute it if it is not a valid CVE ID.

This is the right way to publish a CVE.

## References
- cve.mitre.org(https://cve.mitre.org/cve/researcher_reservation_guidelines){:target="_blank"}