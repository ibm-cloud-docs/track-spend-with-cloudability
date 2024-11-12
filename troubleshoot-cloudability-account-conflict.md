---

copyright:
  years: 2024
lastupdated: "2024-11-12"

keywords: question about {{site.data.keyword.IBM_notm}} Cloudability Enablement

subcollection: track-spend-with-cloudability

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I see conflict Cloudability account conflict in the logs after running the DA?
{: #troubleshoot-cldy-account-conflict}
{: troubleshoot}

The {{site.data.keyword.cloud_notm}} account has already been added to the Cloudability account.
{: shortdesc}

The deployment of the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture failed with the following error message in the schematics logs:
{: tsSymptoms}

```log
Error: unexpected response code '409': {"error":{"status":409,"code":"conflict","messages":["Conflict","A credential for this organization and account already exists."],"uniqueid":"3d36e9d8-90a9-11ef-b8df-9624b4132c80","typeid":"317197432da0a6add4fa95c86d8f35d5","traceid":"3d056f28-90a9-11ef-b8df-9624b4132c80"}}

  with module.cloudability_onboarding[0].restapi_object.cloudability_ibm_account,
  on modules/cloudability-onboarding/main.tf line 38, in resource "restapi_object" "cloudability_ibm_account":
  38: resource "restapi_object" "cloudability_ibm_account" {
```
{: pre}


This is often because the {{site.data.keyword.cloud_notm}} account has already been added to Cloudability, either manually or by another deployment of the DA.
{: tsCauses}

The recommended approach is to delete the existing {{site.data.keyword.cloud_notm}} account from {{site.data.keyword.IBM_notm}} Cloudability and re-run the DA configuration to add the account. This ensures that the vendor credentials within Cloudability are set correctly.
{: tsResolve}

Alternatively, the existing configuration can be manually updated within Cloudability to match the configuration outputs and the adding of the {{site.data.keyword.cloud_notm}} account to Cloudability can be disabled by setting the `cloudability_api_key` parameter in the `Required` tab to `__NULL__`.
