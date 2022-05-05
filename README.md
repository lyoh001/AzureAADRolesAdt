# VICGOV - Azure Active Directory Roles Report
## 1. Introduction
### 1.1	Overview

A number of challenges arise when managing AAD roles across multiple tenants, Hosting Services team have been working to make this process easier to maintain with less administrative overhead.

This document is intended to provide a high level overview of workflow on how the automation notifies the admins with Azure AD roles assigned to all staff in VICGOV.

Included in this report is a step by step detailed guide around where to look for troubleshooting.

## 2 O365 Process Reports (CIS Benchmark)
- Priority: 2
- Description: User role group changes should be reviewed on a weekly basis to ensure no one has been improperly added to an administrative role
- Rationale: llicit role group changes could give an attacker elevated privileges to perform more dangerous and impactful - things in your tenancy.
- Owners: Tier 0
- Notes: Report produced
- Ref: E3_L1
- Summary: A capture (report) of 'odd' role assignments or anomalies (roles assigned outside of scope of PIM).
The report should provide a weekly snapshot of current role assignments and highlight the differences (compared with previous week).
- Considerations: include potential issue where role assignments are made within the week -- i.e., the changes would fall outside of the weekly capture window and therefore not be captured.:



## 3 Logical Architecture
### 3.1	Logical System Component Overview
![Figure 1: Logical Architecture Overview](./.images/workflow.png)
1. Scheduled Job @ 7am on Friday.
2. Function retreives the secrets from the Keyvault.
3. Queries AAD for validating managed identity.
4. Checks AAD for the assigned roles.
5. The function loads prev week's AAD role dataframe from cosmosdb and perform dff comparion check.
6. The notification email gets sent via logic apps with the report attached.