---

copyright:
  years: 2026
lastupdated: "2026-01-09"

keywords: question about {{site.data.keyword.IBM_notm}} Cloudability Enablement

subcollection: track-spend-with-cloudability

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my deployment fail with a timeout when trying to create the object storage bucket?
{: #troubleshoot-bucket-creation-timeout}
{: troubleshoot}

Communication from Schematics to {{site.data.keyword.cos_full_notm}} times out when using the `private` endpoint type.
{: shortdesc}

The deployment of the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture failed with a timeout error when creating the object storage bucket:
{: tsSymptoms}

```log
Terraform apply | module.cos_bucket.module.cos_bucket.ibm_cos_bucket.cos_bucket[0]: Still creating... [02m00s elapsed]
Terraform apply |
Terraform apply | Error: RequestError: send request failed
Terraform apply | caused by: Put "https://s3.private.us-south.cloud-object-storage.appdomain.cloud/billing-reports-edzs": dial tcp 10.1.129.83:443: i/o timeout
Terraform apply |
Terraform apply |   with module.cos_bucket.module.cos_bucket.ibm_cos_bucket.cos_bucket[0],
Terraform apply |   on .terraform/modules/cos_bucket.cos_bucket/main.tf line 122, in resource "ibm_cos_bucket" "cos_bucket":
Terraform apply |  122: resource "ibm_cos_bucket" "cos_bucket" {
Terraform apply |
Terraform apply | ---
Terraform apply | id: terraform-d2853781
Terraform apply | summary: |-
Terraform apply |   RequestError: send request failed
Terraform apply |   caused by: Put "https://s3.private.us-south.cloud-object-storage.appdomain.cloud/billing-reports-edzs": dial tcp 10.1.129.83:443: i/o timeout
Terraform apply | severity: error
Terraform apply | resource: ibm_cos_bucket
Terraform apply | operation: create
Terraform apply | component:
Terraform apply |   name: github.com/IBM-Cloud/terraform-provider-ibm
Terraform apply |   version: 1.79.2
Terraform apply | ---
`{: pre}


Communication from Schematics to {{site.data.keyword.cos_full_notm}} no longer supports the `private` endpoint type and requires either `direct` or `public` endpoint types.
{: tsCauses}

To resolve this issue, upgrade to version `1.2.4` or later of the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture. Version `1.2.4` introduced a fix that changes the default endpoint type to `public` and makes this configurable through the `management_endpoint_type_for_bucket` variable.
{: tsResolve}

If you are using version `1.2.4` or later and the `management_endpoint_type_for_bucket` variable is set to `private`, change this value to either `public` (default) or `direct` in the **Optional** tab of your configuration, then redeploy the deployable architecture.
