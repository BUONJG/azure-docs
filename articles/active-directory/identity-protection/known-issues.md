---
title: FAQs and known issues with identity protection (refreshed) in Azure Active Directory | Microsoft Docs
description: FAQs and known issues with identity protection (refreshed) in Azure Active Directory.
services: active-directory
keywords: azure active directory identity protection, cloud app discovery, managing applications, security, risk, risk level, vulnerability, security policy
documentationcenter: ''
author: MarkusVi
manager: mtillman

ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.subservice: identity-protection
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2019
ms.author: markvi
ms.reviewer: raluthra

ms.collection: M365-identity-device-management
---
# FAQs and known issues with identity protection (refreshed) in Azure Active Directory


## Dismiss user risk

**Dismiss user risk** in classic Identity Protection sets the actor in the user’s risk history in Identity Protection (refreshed) to **Azure AD**.


**Dismiss user risk** in Identity Protection (refreshed) sets the actor in the user’s risk history in Identity Protection (refreshed) to **\<Admin’s name with a hyperlink pointing to user’s blade\>**.

There is a current known issue causing latencies in the user risk dismissal flow. If you have a "User risk policy", this policy will stop applying to dismissed users within minutes of clicking on "Dismiss user risk". However, there are known delays with the UX refreshing the "Risk state" of dismissed users. As a workaround, refresh the page on the browser level to see the latest user "Risk state".


## Risky users report

Queries on the **username** field are case-sensitive, while queries on the **Name** field are case-agnostic.

Toggling **Show dates as** hides the **RISK LAST UPDATED** column. To readd the column click **Columns** at the top of the Risky Users blade.

**Dismiss all events** in classic Identity Protection sets the status of the risk events to **Closed (resolved)**.

If you attempt to access the risky users report by clicking **Risky users report** within a sign-in record in the risky sign-ins report, it may sometimes show **Something went wrong. Please retry**. To remedy this, click **Apply** or **Reset** at the top of the screen and the risky user(s) data will populate.


## Risky sign-ins report

**Resolve** on a risk event sets the status to **Users passed MFA driven by risk-based policy**.

**Reset** in the **Risky Sign-ins** report does not clear the value of the **Risk event type**.


## Frequently asked questions

### Why can’t I set my own risk levels for each risk event?

Risk levels in Identity Protection are based on the precision of the detection and powered by our supervised machine learning. To customize what experience users are presented, administrator can include/exclude certain users/groups from the User Risk and Sign-In Risk Policies.


### Why does the location of a sign-in not match where the user truly signed in from?

IP geolocation mapping is an industry-wide challenge. If you feel that the location listed in the sign-ins report does not match the actual location, please reach out to support. 


### How do the feedback mechanisms in Identity Protection work?

**Confirm compromised** (on a sign-in) – Informs Azure AD Identity Protection that the sign-in was not performed by the identity owner and indicates a compromise.

- Upon receiving this feedback, we move the sign-in and user risk state to **Confirmed compromised** and risk level to **High**.

- In addition, we provide the information to our machine learning systems for future improvements in risk assessment.

    > [!NOTE]
    > If the user is already remediated, don't click **Confirm compromised** because it moves the sign-in and user risk state to **Confirmed compromised** and risk level to **High**.

**Confirm safe** (on a sign-in) – Informs Azure AD Identity Protection that the sign-in was performed by the identity owner and does not indicate a compromise.

- Upon receiving this feedback, we move the sign-in (not the user) risk state to **Confirmed safe** and the risk level to **-**.

- In addition, we provide the information to our machine learning systems for future improvements in risk assessment.

    > [!NOTE]
    > If you believe the user is not compromised, use **Dismiss user risk** on the user level instead of using **Confirmed safe** on the sign-in level. A **Dismiss user risk** on the user level closes the user risk and all past risky sign-ins and risk events.



### Why am I seeing a user with a low (or above) risk score, even if no risky sign-ins or risk events are shown in Identity Protection?

Given the user risk is cumulative in nature and does not expire, a user may have a user risk of low or above even if there are no recent risky sign-ins or risk events shown in Identity Protection. This could happen if the only malicious activity on a user took place beyond the timeframe for which we store the details of risky sign-ins and risk events. We do not expire user risk because bad actors have been known to stay in customers' environment over 140 days behind a compromised identity before ramping up their attack. Customers can review the user's risk timeline to understand why a user is at risk by going to: `Azure Portal > Azure Active Directory > Risky users’ report > Click on an at-risk user > Details’ drawer > Risk history tab`

### Why does a sign-in have a “sign-in risk (aggregate)” score of High when the detections associated with it are of low or medium risk?

The high aggregate risk score could be based on other features of the sign-in, or the fact that more than one detection fired for that sign-in. And conversely, a sign-in may have a sign-in risk (aggregate) of Medium even if the detections associated with the sign-in are of High risk. 
