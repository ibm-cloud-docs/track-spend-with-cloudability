---

copyright:
  years: 2024
lastupdated: "2024-11-27"

keywords:

subcollection: track-spend-with-cloudability

---

{{site.data.keyword.attribute-definition-list}}

# Deploying with {{site.data.keyword.cloud_notm}} projects
{: #deploy-cloud}

Deploying with {{site.data.keyword.cloud_notm}} Projects ensures that your infrastructure is managed, secure, and always compliant by using infrastructure as code (IaC) and integrated compliance tools. For more information, see [Learn about IaC deployments with projects](/docs/secure-enterprise?topic=secure-enterprise-understanding-projects).


## Before you begin
{: #required-access-for-projects}

Ensure that you created [iam credentials](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning) to authorize the project deployment and have the permissions to create a project in the desired account. These access permissions include:

- The Editor role on the Projects service
- The Editor and Manager role on the {{site.data.keyword.bpshort}} service
- The Viewer role on the resource group for the project

For more information, see [Assigning users access to projects](/docs/secure-enterprise?topic=secure-enterprise-access-project).

### Running the {{site.data.keyword.IBM_notm}} Cloudability Enablement DA
{: #running-cloudability-enablement}

Complete the following steps to run the Cloudability Enablement DA with {{site.data.keyword.cloud_notm}} Projects:

1.  From the {{site.data.keyword.cloud_notm}} [catalog](/catalog?search=Cloudability%20Enablement%20label%3Adeployable_architecture#search_results){: external}, search for Cloudability Enablement, and click the tile for the DA.
2.  Select the latest product version from the Architecture section.
3.  Click `Add to project`.
    1.  Name your project, enter a description, and specify a configuration name. Then, click `Create`.
    2.  Select the region and the resource group where project artifacts must be stored.
4.  Edit and validate the configuration:
    1.  Select your authentication method that corresponds to your iam operator that was [previously configured](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning#cloudability-iam-prereqs). You can use a trusted profile, an existing secret in {{site.data.keyword.secrets-manager_short}}, or add your API key directly. For more information see: [Using an API key or secret to authorize projects](/docs/secure-enterprise?topic=secure-enterprise-authorize-project).
    2.  On the `Required` tab, enter the `cloudability_api_key` with the api key from the [Cloudability account preferences](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning#api-key).
    3.  If the {{site.data.keyword.cloud_notm}} account is an enterprise account, then set `is_enterprise_account` to `True` and on the `Optional` tab enter in the value of the `enterprise_id`, which is available in the enterprise details of your [enterprise dashboard](/enterprise)
    4.  Optionally, update any other parameters. See the [configuration reference](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-configure) for documentation on the available parameters.
    5.  Save the configuration.
    6.  Click `Validate`. Validation takes a few minutes.

        {{site.data.keyword.cloud_notm}} Projects run a Security and Compliance Center (SCC) scan against the {{site.data.keyword.cloud_notm}} for Financial Services profile. Controls that are part of the DA and are included in the list of supported {{site.data.keyword.compliance_short}} rules are checked when you validate the configuration.
{: important}

5.  Deploy the configuration. After you validate your configuration, you can deploy it to your target account:

    1.  Review the input values and make any necessary changes.
    2.  Click `Deploy`. Deploying the DA can take a few minutes. You are notified when the deployment is successful.

6.  Review the outputs from the DA.

7.  You can validate that the connection to {{site.data.keyword.cloud_notm}} was completed in Cloudability under [`Vendor Credentials`](https://app.apptio.com/cloudability#/credentials/ibm)

During the validation and deployment process, monitor the [needs attention items](/docs/secure-enterprise?topic=secure-enterprise-needs-attention-projects). The widget reflects any issue that occurs in your configurations.
{: remember}

## Next Steps
{: #deploy-next-steps}

Congratulations your {{site.data.keyword.cloud_notm}} account should now be added to Cloudability. Your billing data from your account should appear in Cloudability within 24 hours. You can also request that up to a year of [historical data be added to your bucket](/docs/account?topic=account-exporting-your-usage&interface=ui#access-historical-data). If you experience any issues during the validation stage, consult the [getting help and support guide](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-help-and-support).
