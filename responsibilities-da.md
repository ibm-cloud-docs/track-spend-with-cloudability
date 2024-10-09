---

copyright:
  years: 2023
lastupdated: "2024-10-09"

subcollection: track-spend-with-cloudability

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Understanding your responsibilities when you use {{site.data.keyword.IBM_notm}} Cloudability Enablement
{: #responsibilities}



Learn about the management responsibilities and terms and conditions that you have when you use the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture (DA).
{: shortdesc}

- For more information about the responsibilities for you and for {{site.data.keyword.IBM}} when you use a DA, see [Understanding your responsibilities when you use DA](/docs/secure-enterprise?topic=secure-enterprise-responsibilities-deployable-architectures).
- For a high-level view of the service types in {{site.data.keyword.cloud}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for using {{site.data.keyword.cloud}} products](/docs/overview?topic=overview-shared-responsibilities).
- For the overall terms of use, see [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview?topic=overview-terms).



Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use the {{site.data.keyword.IBM_notm}} Cloudability Enablement DA.





## Incident and operations management
{: #incident-and-ops}




Incident and operations management includes tasks such as monitoring, event management, high availability, problem determination, recovery, and full state backup and recovery.

|  | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Task 1| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
|Task 2| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
|Task 3| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
{: row-headers}
{: caption="Responsibilities for incident and operations" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}


## Change management
{: #change-management}






Change management includes tasks such as deployment, configuration, upgrades, patching, configuration changes, and deletion.

|  | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Task 1| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
|Task 2| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
|Task 3| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
{: row-headers}
{: caption="Responsibilities for change management" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}


## Identity and access management
{: #iam-responsibilities}




Identity and access management includes tasks such as authentication, authorization, access control policies, and approving, granting, and revoking access.

|  | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Secure with least privilege | Document the minimal IAM access requirements to run the DA. |  |
| Manage secrets | | * Generate the necessary secrets (IAM API keys) and configure trusted profiles that are required for the DA. \n * Manage generated secrets by following secure best practices. |
{: row-headers}
{: caption="Responsibilities for identity and access management" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}

## Security and regulation compliance
{: #security-compliance}




Security and regulation compliance includes tasks such as security controls implementation and compliance certification.

|  | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Meet security and compliance objectives | Provide a secure DA that complies with declared standards. For more information about data security, see [How do I know that my data is safe?](/docs/overview?topic=overview-security).
| Verify configuration changes | | Understand the effects on the security and compliance posture of any user-initiated changes to the default configuration. Run {{site.data.keyword.compliance_long}} checks if needed to ensure that the DA remains in compliance. |
{: row-headers}
{: caption="Responsibilities for security and regulation compliance" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}

## Disaster recovery
{: #disaster-recovery}




Disaster recovery includes tasks such as providing dependencies on disaster recovery sites, provision disaster recovery environments, data and configuration backup, replicating data and configuration to the disaster recovery environment, and failover on disaster events.

The {{site.data.keyword.IBM_notm}} Cloudability Enablement DA does not identify specific responsibilities in this area. For information about the general BCDR responsibilities, when you use IBM deployable architectures, see [Disaster recovery](/docs/secure-enterprise?topic=secure-enterprise-responsibilities-deployable-architectures#disaster-recovery-da).
