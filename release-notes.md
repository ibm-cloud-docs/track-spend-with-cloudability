---

copyright:
  years: 2024
lastupdated: "2024-12-10"

keywords:

subcollection: track-spend-with-cloudability

content-type: release-note

---



{{site.data.keyword.attribute-definition-list}}



# Release notes for {{site.data.keyword.IBM_notm}} Cloudability Enablement
{: #cloudability-relnotes}



Use these release notes to learn about the latest updates to the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture. Each release is grouped by the date. Release notes are available for a minimum of three years.
{: shortdesc}



## December 2024
{: #subcollection-nov2024}

### 13 Dec 2024
{: #subcollection-13dec2024}
{: initial-release}

Version 1.0.21 of the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture is available
: The {{site.data.keyword.IBM_notm}} Cloudability Enablement architecture is the easiest way to add your {{site.data.keyword.cloud_notm}} account or enterprise to an existing {{site.data.keyword.IBM}} Cloudability account.

## Source Dependencies
{: #attribution}

The {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture uses the following dependencies:


| Terraform Provider | Version  |
| :----------------- | :------- |
| [IBM-Cloud/ibm](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest)      | >=1.71.0 |
| [Mastercard/restapi](https://registry.terraform.io/providers/Mastercard/restapi/latest) | 1.20.0               |
| [skyscrapr/terraform-provider-cloudability](https://registry.terraform.io/providers/skyscrapr/cloudability/latest) | 0.0.40               |
{: caption="Terraform provider dependencies" caption-side="bottom"}


| Terraform Modules | Version  |
| :----------------- | :------- |
| [terraform-ibm-modules/resource-group/ibm](https://registry.terraform.io/modules/terraform-ibm-modules/resource-group/ibm/latest)      | >=1.1.6 |
| [terraform-ibm-modules/cos/ibm](https://registry.terraform.io/modules/terraform-ibm-modules/cos/ibm/latest)      | >=8.15.2 |
| [terraform-ibm-modules/kms-all-inclusive/ibm](https://registry.terraform.io/modules/terraform-ibm-modules/kms-all-inclusive/ibm/latest)      | >=4.17.1 |
{: caption="Terraform modules" caption-side="bottom"}
