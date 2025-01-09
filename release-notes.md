---

copyright:
  years: 2025
lastupdated: "2025-01-09"

keywords:

subcollection: track-spend-with-cloudability

content-type: release-note

---



{{site.data.keyword.attribute-definition-list}}



# Release notes for {{site.data.keyword.IBM_notm}} Cloudability Enablement
{: #cloudability-relnotes}



Use these release notes to learn about the latest updates to the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture. Each release is grouped by the date. Release notes are available for a minimum of three years.
{: shortdesc}


## January 2025
{: #subcollection-jan2025}

### 10 Jan 2025
{: #subcollection-10jan2025}

Version 1.1.0 of the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture (DA) is available
: Added support for Access Administration authentication, which uses a more secure token-based authentication as opposed to the basic authentication used by Cloudability API key. See the [Access Administration overview and FAQ](https://help.apptio.com/en-us/frontdoor/admin-guide/eaa-api/overview-api-keys-faq.html){: external} within the Apptio Help Center for more details.
To switch to using Access Administration authentication, use the following steps to [configure the deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-config-project&interface=ui).

1. Follow the [acquiring access administration API key](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning#frontdoor-api-key) guide to create the API key within Apptio.
2. Edit the DA configuration within IBM Cloud:
    1. Select the project with the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture (DA) from the [projects list](/projects)
    2. Go to the Configurations tab. Select the configuration corresponding to the Cloudability Enablement deployable architecture.
    3. Click the **Edit** button.
3. On the **Required** tab of the DA configuration page within IBM Cloud, select the `Access Administration Authentication` option for the `cloudability_auth_type`.
4. Enter the `frontdoor_public_key`, `frontdoor_secret_key`, and `cloudability_environment_id` created in step 1.
5. Click the **Save** button
6. Click the **Validate** button. A modal dialog is displayed which provides more details about your in-progress validation.

In addition, `cloudability_auth_type` can be set to `none`, or `manual`.

* `none`: disables any connection to Cloudability so that the DA can be used as a way to configure [export billing reports to Cloud Object Storage](/docs/account?topic=account-exporting-your-usage&interface=ui#enable-export-usage)
* `manual`: Creates billing exports as in the case or `none`but also grants Cloudability access to the Object Storage bucket, but the DA does not add the IBM Cloud account to Cloudability. Use this option to manually add the IBM Cloud account to Cloudability through its UI.

#### Inputs Added
{: #subcollection-13jan2025-inputs}

* `cloudability_auth_type`
* `frontdoor_public_key`
* `frontdoor_secret_key`
* `cloudability_environment_id`

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
| [IBM-Cloud/ibm](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest)      | `>=1.73.0` |
| [Mastercard/restapi](https://registry.terraform.io/providers/Mastercard/restapi/latest) | `1.20.0`               |
| [skyscrapr/terraform-provider-cloudability](https://registry.terraform.io/providers/skyscrapr/cloudability/latest) | `0.0.40`               |
{: caption="Terraform provider dependencies" caption-side="bottom"}


| Terraform Modules | Version  |
| :----------------- | :------- |
| [terraform-ibm-modules/resource-group/ibm](https://registry.terraform.io/modules/terraform-ibm-modules/resource-group/ibm/latest)      | `>=1.1.6` |
| [terraform-ibm-modules/cos/ibm](https://registry.terraform.io/modules/terraform-ibm-modules/cos/ibm/latest)      | `>=8.16.4` |
| [terraform-ibm-modules/kms-all-inclusive/ibm](https://registry.terraform.io/modules/terraform-ibm-modules/kms-all-inclusive/ibm/latest)      | `>=4.19.1` |
{: caption="Terraform modules" caption-side="bottom"}
