---

copyright:
  years: 2024
lastupdated: "2024-11-12"

subcollection: track-spend-with-cloudability

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Understanding your responsibilities when you use {{site.data.keyword.IBM_notm}} Cloudability Enablement
{: #responsibilities}



Learn about the management responsibilities and terms and conditions that you have when you use the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture (DA).
{: shortdesc}

- For more information about the responsibilities for you and for {{site.data.keyword.IBM}} when you use a DA, see [Understanding your responsibilities when you use DA](/docs/secure-enterprise?topic=secure-enterprise-responsibilities-deployable-architectures).
- For a high-level view of the service types in {{site.data.keyword.cloud}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see "[Shared responsibilities for using {{site.data.keyword.cloud}} products](/docs/overview?topic=overview-shared-responsibilities)".
- For the overall terms of use, see [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview?topic=overview-terms).



Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use the {{site.data.keyword.IBM_notm}} Cloudability Enablement DA.





## Incident and operations management
{: #incident-and-ops}




Incident and operations management includes tasks such as monitoring, event management, high availability, problem determination, recovery, and full state backup and recovery.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Configuring Activity tracker audit logging| Provide the [activity tracker configuration variables](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-bucket-audit-events), which are enabled by default | Review and disable these configurations as desired and [configure a target](/docs/atracker?topic=atracker-getting-started-target-cloud-logs) to view the logs |
|Configuring Monitoring |Provide the [monitoring configuration variables](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-bucket-metrics), which are enabled by default | 1. Review and disable these configurations as desired.<br /> 2. Configure a [metrics target](/docs/metrics-router?topic=metrics-router-target-manage&interface=ui). |
|Key Project failover| Support configuration of {{site.data.keyword.keymanagementserviceshort}} failover regions for {{site.data.keyword.cos_full_notm}} encryption | Selecting one of the [supported {{site.data.keyword.keymanagementserviceshort}} failover regions](/docs/key-protect?topic=key-protect-ha-dr#availability) when [configuring the region](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-regions) of the deployed infrastructure if {{site.data.keyword.keymanagementserviceshort}} failover support if needed. |
{: row-headers}
{: caption="Responsibilities for incident and operations" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or {{site.data.keyword.IBM_notm}} might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}


## Change management
{: #change-management}






The {{site.data.keyword.IBM_notm}} Cloudability Enablement DA does not identify specific responsibilities in this area. For information about the general change management responsibilities when you use {{site.data.keyword.IBM_notm}} deployable architectures, see [Change management](/docs/secure-enterprise?topic=secure-enterprise-responsibilities-deployable-architectures#change-management-da).


## Identity and access management
{: #iam-responsibilities}




Identity and access management includes tasks such as authentication, authorization, access control policies, and approving, granting, and revoking access.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Secure with least privilege | Documenting and maintaining the minimal IAM access requirements to run the DA. | Ensure that the DA operator is [configured with the least privileged access policies](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-cloudability-iam-prereqs) |
| Manage secrets | | * Generate the necessary secrets (IAM API keys) and configure trusted profiles that are needed to run the DA. <br /> * Manage generated secrets by following secure best practices such as rotating credentials. |
| {{site.data.keyword.cos_short}} Billing Report Access | | Administrating access to the {{site.data.keyword.cos_full_notm}}, which contains the {{site.data.keyword.IBM_notm}} billing reports |
{: row-headers}
{: caption="Responsibilities for identity and access management" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or {{site.data.keyword.IBM_notm}} might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}

## Security and regulation compliance
{: #security-compliance}




Security and regulation compliance includes tasks such as security controls implementation and compliance certification.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Meet security and compliance objectives | Provide a secure DA that complies with declared standards. For more information about data security, see "[How do I know that my data is safe?](/docs/overview?topic=overview-security)". | |
| Verify configuration changes | | Understand the effects on the security and compliance posture of any user-initiated changes to the default configuration. Run {{site.data.keyword.compliance_long}} checks if needed to ensure that the DA remains in compliance. |
{: row-headers}
{: caption="Responsibilities for security and regulation compliance" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or {{site.data.keyword.IBM_notm}} might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}

## Disaster recovery
{: #disaster-recovery}




Disaster recovery includes tasks such as providing dependencies on disaster recovery sites, provision disaster recovery environments, data and configuration backup, replicating data and configuration to the disaster recovery environment, and failover on disaster events.

The {{site.data.keyword.IBM_notm}} Cloudability Enablement DA does not identify specific responsibilities in this area. For information about the general BCDR responsibilities when you use {{site.data.keyword.IBM_notm}} deployable architectures, see [Disaster recovery](/docs/secure-enterprise?topic=secure-enterprise-responsibilities-deployable-architectures#disaster-recovery-da).
