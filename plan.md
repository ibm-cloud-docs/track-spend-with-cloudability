---

copyright:
  years: 2025
lastupdated: "2025-01-13"

keywords:

subcollection: track-spend-with-cloudability

---


{{site.data.keyword.attribute-definition-list}}

# Setting up {{site.data.keyword.IBM_notm}} Cloudability Enablement Deployable Architecture
{: #planning}

Running the {{site.data.keyword.IBM_notm}} Cloudability Enablement Deployable Architecture(DA) requires authorization inputs from the {{site.data.keyword.cloud_notm}} account. An {{site.data.keyword.IBM_notm}} Cloudability API key is also needed to add your {{site.data.keyword.cloud_notm}} account to {{site.data.keyword.IBM_notm}} Cloudability. Follow these instructions to help create and manage your [API keys](#x8051010){: term}.
{: shortdesc}

Authentication to {{site.data.keyword.IBM_notm}} Cloudability is not required to run the deployable architecture. You can configure the deployable architecture(DA) to create the infrastructure and manually add the {{site.data.keyword.cloud_notm}} account to Cloudability through its UI or re-configure the DA to add the {{site.data.keyword.cloud_notm}} account to Cloudability later. See the [Cloudability configuration reference](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-configure) for more details.
{: notice}

## Cloudability authorization
{: #api-key}

The Cloudability Enablement DA supports two types of authentication to Cloudability:

1. [Cloudability API key](#acquiring-api-key) (simpler)
2. [Access Administration API key](#frontdoor-api-key) (more secure)

You must use the Access Administration API key approach to authenticate with Cloudability if you are using a GovCloud Cloudability environment.
{: notice}

### Before you begin
{: #cloudability-api-key-before-you-begin}

Ensure that your Cloudability user has an **Administrator** role so that it has sufficient permissions to add vendor accounts to Cloudability. If you don't have access to a Cloudability account, then visit the guide on [accessing your Cloudability account](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-accessing-cloudability).

Create your API Key as a functional user (for example: **cloudability-integration**) with access to add cloud vendors.
{: recommend}

Securely store your API Key in [{{site.data.keyword.cloud_notm}} Secrets Manager](/docs/secrets-manager?topic=secrets-manager-getting-started) as an arbitrary key. Secrets Manager makes it easier to rotate the API key and allows it to be referenced in [{{site.data.keyword.IBM}} Projects](/docs/secure-enterprise?topic=secure-enterprise-project-faqs#project-log-issue) without exposing the key in your DA configurations.
{: recommend}

### Option 1: Acquiring a Cloudability api key
{: #acquiring-api-key}

The Cloudability API key is the easiest way to authenticate with Cloudability. However, it is considered less secure than using the Frontdoor open token authentication.
A logged in user can retrieve a Cloudability API key from the [Cloudability account preferences](https://app.apptio.com/cloudability#/settings/preferences). Use the following steps to create your API key:

1. Log in to your [Cloudability account](https://frontdoor.apptio.com/login/).
2. Click the profile icon in the upper right corner to navigate to the **Settings** page.
3. Select **Manage Profile**.
4. Select the **Preferences** tab to reveal the **Cloudability API** section on the right.
5. If an API Key is not viewable, click **Enable Access** to reveal the API Key displayed in the text box.
6. Copy and securely store the API Key for the next step of [configuring the DA](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-deploy-cloud).

See the [Cloudability getting started API documentation](https://help.apptio.com/en-us/cloudability/api/v3/getting%20started%20with%20the%20cloudability.htm){: external} for more details.

### Option 2: Acquiring an Access Administration API key
{: #frontdoor-api-key}

The Access Administration API key is the more secure approach to authenticate with Cloudability. It also allows creating multiple api keys, which can be used to rotate API Keys. However, using Access Administration authentication requires additional inputs to configure the deployable architecture.

A logged in user can create an Access Administration API key from the [frontdoor user profile](https://frontdoor-ui.apptio.com/profile?tab=apiKeys). Use the following steps to create your API key:

1. In the [**User Profile** page](https://frontdoor-ui.apptio.com/profile), select the **API Keys** tab.
2. Select **Create API Key**, which displays a dialog.
3. Type a **Key Name** and **Description**.
4. Select an expiration policy, and select **Confirm**.
5. Note the public key. Select the ![copy icon](./images/copy.svg) to copy the secret key. You can only access the secret key while creating the API key. Store the public key and secret key as an arbitrary key in Secrets Manager to be accessed later.
6. Click **Grant Access** on the newly created API Key in the table of API Keys
7. Select the desired environment from the list of environments and then click **Next**
8. Select roles for the API key. Select **Next**, and then select **Confirm**.
9. In the [**User Profile** page](https://frontdoor-ui.apptio.com/profile), select the **Environment Access** tab.
10. Note the Environment Id below the environment name in the table of Environments and the corresponding API Keys. Save the Environment Id when [configuring the DA](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-deploy-cloud).

See the [Cloudability access administration documentation](https://help.apptio.com/en-us/frontdoor/admin-guide/eaa-api/overview-api-keys-faq.html#CreateandmanageAccessAdministrationAPIkeys){: external} for more details and FAQ on Access Administration API keys.


## Configuring {{site.data.keyword.cloud_notm}} IAM permissions
{: #cloudability-iam-prereqs}

Authorization needs to be granted to either a trusted profile, user, or service ID, which is referred to as an operator. This operator is [associated with the Project](/docs/secure-enterprise?topic=secure-enterprise-authorize-project) so that it has the permissions to run the Cloudability deployable architecture.

For enterprise accounts the IAM credentials only need to be configured in the primary Enterprise account to allow {{site.data.keyword.IBM_notm}} Cloudability to access billing reports for all current and future accounts within the {{site.data.keyword.cloud_notm}} Enterprise. It is unnecessary to independently add each account within the enterprise.
{: important}

### Before you begin
{: #iam-before-you-begin}

If you have the following access, you can create access credentials to run the DA:

- Account owner
- Administrator role on all account management services
- Administrator role on the IAM Identity Service. For more information, see [IAM Identity service](/docs/account?topic=account-account-services#identity-service-account-management)


### Required policies
{: #required-policies}

Add the access policies to an [access group](/docs/account?topic=account-groups) rather than directly adding the policies to your DA operator (trusted profile, user, or service ID.).
{: recommend}

The following access policies are necessary to run the DA.

| Service | Platform Roles | Service Roles | Reason |
|------|-------------|------|---------|
| `{{site.data.keyword.cos_full_notm}}` | `Administrator` | `Writer`, `ObjectReader` | The `Writer` role is needed to create/delete and configure a bucket in a {{site.data.keyword.cos_short}} instance. The `Administrator` role is needed to create the iam policy, which grants {{site.data.keyword.cloud_notm}} access to read the billing reports in the bucket and to create the service authorization between Billing and {{site.data.keyword.cos_full_notm}}. `ObjectReader` is needed to read the list of objects in the bucket in order to validate that billing reports are added to the bucket. |
| `{{site.data.keyword.keymanagementserviceshort}}` | `Editor` | `Manager` | Used to create a key and key ring in a {{site.data.keyword.keymanagementserviceshort}} instance for bucket encryption. |
| `Billing` | `Administrator` | N/A | Used to configure account billing exports to the {{site.data.keyword.cos_full_notm}} bucket |
| `IAM Access Management` | `Administrator` | N/A | 1. Create custom iam roles for least privileged access for {{site.data.keyword.IBM_notm}} Cloudability.\n 2. Create service authorizations between {{site.data.keyword.cos_short}} and {{site.data.keyword.keymanagementserviceshort}} and between Billing and {{site.data.keyword.cos_full_notm}}.\n 3. Ability to grant policies to the Cloudability service ID to read the billing reports from the bucket. |
| `Enterprise` | `Administrator` | N/A | Only for enterprise accounts. Used to manage the iam policy for {{site.data.keyword.IBM_notm}} Cloudability to view the list of child accounts. |
| `All Account Management` | `Administrator` | N/A | Only if the DA is creating a new Resource Group to provision resources. `Administrator` is needed (as opposed to the `Editor` role) to delete the resource group in the event of deprovisioning. Alternatively resources can be placed in an existing resource group in which case access needs to be granted to that resource group. See [giving access to resources in resource groups](/docs/account?topic=account-rgs_manage_access&interface=ui) for more details. |
{: caption="Access Policies" caption-side="bottom"}

### Using an access groups
{: #access-groups}

1. [Create an access group](/docs/account?topic=account-groups&interface=ui#create_ag)
2. Assign the access policies from [Table 1](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning#iam-before-you-begin) to the access group.
3. Add the Operator (user, service ID, trusted profile) as a [member of the access group](/docs/account?topic=account-groups&interface=ui#add-users-ag).
4. Create an API Key if the Operator is a [user](/docs/account?topic=account-userapikey&interface=ui) or [service ID](/docs/account?topic=account-serviceidapikeys&interface=ui). Alternatively use [{{site.data.keyword.IBM_notm}} Secrets Manager to manage the IAM credentials](/docs/secrets-manager?topic=secrets-manager-iam-credentials&interface=ui) of your service ID.

It is recommended to store any user or service [API keys in Secrets Manager](/docs/secure-enterprise?topic=secure-enterprise-authorize-project&interface=ui). Secrets manager allows you to easily rotate credentials and prevents exposing highly privileged credentials to any users who are responsible for the running and management of the project that is used to run the DA.
{: recommend}


### Using a trusted profile
{: #trusted-profile}

1. [Create a Project](/docs/secure-enterprise?topic=secure-enterprise-setup-project)
2. [Create a Trusted Profile for the Project](/docs/secure-enterprise?topic=secure-enterprise-tp-project#create-projects-tp)
3. Assign the access policies from [Table 1](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning#iam-before-you-begin) and the [trusted profile policies that are needed by Projects](/docs/secure-enterprise?topic=secure-enterprise-tp-project#create-projects-tp) to the trusted profile.
4. Copy the [the trusted profile ID](/docs/secure-enterprise?topic=secure-enterprise-tp-project#find-tp-id) for the next step to [deploy the DA](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-deploy-cloud)

## Next steps
{: #planning-next-steps}

You are now ready to [run the deployable architecture](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-deploy-cloud) by using {{site.data.keyword.cloud_notm}} Projects.
