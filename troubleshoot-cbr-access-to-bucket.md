---

copyright:
  years: 2026
lastupdated: "2026-01-06"

keywords: question about {{site.data.keyword.IBM_notm}} Cloudability Enablement

subcollection: track-spend-with-cloudability

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I access the billing reports objects in my storage bucket?
{: #troubleshoot-access-billing-report-objects}
{: troubleshoot}

The IBM Cloudability Enablement deployable architecture was deployed successfully but access is restricted to view the billing report files within the bucket.
{: shortdesc}

When viewing the contents of the billing reports storage bucket within the IBM Cloud console, you see the error notification:
{: tsSymptoms}

```log
Access denied
BMCOSUI020001: Your attempt to fetch objects failed. Please contact your administrator for access.
```
{: pre}

The most likely cause is that you are denied because of a [context-based restriction (CBR)](/docs/account?topic=account-context-restrictions-whatis). By default the Cloudability Enablement deployable architecture creates a CBR to limit access to only IBM Cloudability, the IBM Cloud billing service, and IBM Cloud Schematics.
{: tsCauses}

To resolve the issue, you can do one of two things:

1. Disable the context-based restriction from within the Project configuration.
2. Add an existing or new CBR zone with the IP addresses of your company to the CBR rule.
{: tsResolve}

Context-based restrictions work with IAM policies to enforce access. Therefore, a user must meet both the requirements of the IAM policies and use an allowed IP address to view the contents of the bucket.
{: note}

To disable the context-based restrictions on the Object Storage bucket, set the variable `cbr_enforcement_mode` to either `disabled` or `report`.
To create a CBR zone with access to the bucket, add the range of IP addresses to the configuration variable `additional_allowed_cbr_bucket_ip_addresses`.
If you want to grant an existing CBR zone to have access to the bucket then add the ID of the zone in the configuration variable `existing_allowed_cbr_bucket_zone_id`.

For more details on the available CBR configuration variables, see the [configuration reference](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-configure#cbr-config
)
To learn how to configure these variables in the project configuration, see [Configuring an architecture by using the console](/docs/secure-enterprise?topic=secure-enterprise-config-project&interface=ui#how-to-config).
