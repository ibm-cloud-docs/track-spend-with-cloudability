---

copyright:
  years: 2024
lastupdated: "2024-10-09"

keywords:

subcollection: track-spend-with-cloudability

---


{{site.data.keyword.attribute-definition-list}}

# Required Access to run {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture(DA)
{: #planning}

The {{site.data.keyword.IBM_notm}} Cloudability Enablement DA requires two credentials to run:
1. An {{site.data.keyword.Bluemix_notm}} API Key or a trusted profile with sufficient privileges to run the DA
2. An {{site.data.keyword.IBM_notm}} Cloudability api key with authorization to add the {{site.data.keyword.Bluemix_notm}} account



## Setup the {{site.data.keyword.Bluemix_notm}} projects for deploying in the {{site.data.keyword.Bluemix_notm}} target account
{: #cloudability-projects-prereqs}

Before creating a project to manage the {{site.data.keyword.IBM_notm}} Cloudability Enablement DA, you must authorize the deployment.

You can authorize the deployments by [using an API key with Secrets Manager to authorize a project to deploy an architecture](/docs/secure-enterprise?topic=secure-enterprise-authorize-project&interface=ui) or [configuring a trusted profile](/docs/secure-enterprise?topic=secure-enterprise-tp-project&interface=ui) with the {{site.data.keyword.Bluemix_notm}} target account.


## Set the IAM permissions
{: #cloudability-iam-prereqs}

User access to {{site.data.keyword.cloud_notm}} resources is controlled by using the access policies that are assigned to access groups. For {{site.data.keyword.cloud_notm}} Financial Services validation, do not assign direct IAM access to any {{site.data.keyword.cloud_notm}} resources. You can set up one access group for the users that can deploy the solution.

IAM access roles are required to install this DA and create all the required elements in the {{site.data.keyword.Bluemix_notm}} target account:

You need the following permissions to run this DA:

- IAM services
    - **Cloud Object Storage** service
        - `Administrator` platform access
        - `Manager` service access
    - **Key Protect** service
        - `Editor` platform access
        - `Manager` service access
- Account management services
    - **Billing** service
        - `Administrator` platform access
    - **Enterprise** service (only for enterprise accounts)
        - `Viewer` platform access
    - **IAM Access Management** service (only for enterprise accounts)
        - `Administrator` platform access



## Cloudability Api Key Access
{: #cloudability-api-key}

To create your {{site.data.keyword.IBM_notm}} Cloudability API key:

1. [Log in](https://frontdoor.apptio.com/login/) to your Cloudability account.
2. Navigate to the Settings menu by clicking on the profile icon in the top right corner and select "Manage Profile".
3. Select the "Preferences" tab to reveal the "Cloudability API" on the right.
4. If an API Key is not viewable, click "Enable Access" to reveal the API Key.
5. Copy this API key or securely store the API Key in [{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.secrets-manager_short}}](/docs/secrets-manager?topic=secrets-manager-getting-started) for use in the DA configuration.

Recommendations:
- Use a functional user for the API key (e.g., "cloudability-integration-key").
- Ensure the user creating the key has permissions to add cloud vendors.
- Securely store this API Key in [{{site.data.keyword.Bluemix_notm}} Secrets Manager](/docs/secrets-manager?topic=secrets-manager-getting-started) as an arbitrary key. Regularly rotate the API key for security.
