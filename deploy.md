---

copyright:
  years: 2024
lastupdated: "2024-10-09"

keywords:

subcollection: track-spend-with-cloudability

---

{{site.data.keyword.attribute-definition-list}}

# Connecting {{site.data.keyword.IBM_notm}} Cloudability to your {{site.data.keyword.Bluemix_notm}} Account or Enterprise
{: #deploy}

You can deploy a deployable architecture(DA) from the {{site.data.keyword.cloud_notm}} catalog. You can choose from different deployment options, including an option to deploy with {{site.data.keyword.cloud_notm}} projects. For more information, see [Learn about IaC deployments with projects](/docs/secure-enterprise?topic=secure-enterprise-understanding-projects).

## Deploying with {{site.data.keyword.cloud_notm}} projects
{: #deploy-cloud}

### Access for {{site.data.keyword.cloud_notm}} projects
{: #required-access-for-projects}

You should use {{site.data.keyword.cloud_notm}} projects as a deployment option. Projects are designed with infrastructure as code and compliance in mind to help ensure that your projects are managed, secure, and always compliant. For more information, see [Learn about IaC deployments with projects](/docs/secure-enterprise?topic=secure-enterprise-understanding-projects).

The {{site.data.keyword.Bluemix_notm}} account where your project is located might be different than the {{site.data.keyword.Bluemix_notm}} target account where you are going to install the {{site.data.keyword.IBM_notm}} Cloudability Enablement DA. The following information refers to the permissions you must have in the project account to create a project and create project tools resources within the account. Make sure that you have the following access:

- The Editor role on the Projects service
- The Editor and Manager role on the {{site.data.keyword.bpshort}} service
- The Viewer role on the resource group for the project

For more information, see [Assigning users access to projects](/docs/secure-enterprise?topic=secure-enterprise-access-project).

### Deploying using {{site.data.keyword.cloud_notm}} projects
{: #deploy-with-projects}



To deploy the {{site.data.keyword.IBM_notm}} Cloudability Enablement DA through the {{site.data.keyword.cloud_notm}} catalog, complete the following steps:
1.  Make sure that you comply with the prerequisites outlined in the [planning](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning) topic.
2.  From the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}, search for Cloudability Enablement, and click the tile for the DA.
4.  Select the latest product version from the Architecture section.
5.  Select a variation, if more than one is available.
6.  Click **Add to project**.
    1.  Name your project, enter a description, and specify a configuration name. Then, click **Create**.
    2.  Select the region and the resource group where project artifacts must be stored.
1.  Edit and validate the configuration:
    1.  Select your authentication method. You can use a trusted profile or an existing secret in {{site.data.keyword.secrets-manager_short}}. Alternatively, you can add your API key directly, which is not recommended. For more information, see [Using an API key or secret to authorize projects](/docs/secure-enterprise?topic=secure-enterprise-authorize-project).
    1.  Enter the Cloudability API key from the Required tab.
    1.  If the {{site.data.keyword.Bluemix_notm}} Account is an Enterprise Account then from the Optional tab set `is_enterprise_account` to `True`
    4.  Save the configuration.
    5.  Click **Validate**. Validation takes a few minutes.

        {{site.data.keyword.cloud_notm}} projects runs an SCC scan against the {{site.data.keyword.cloud_notm}} for Financal Services profile. Controls that are part of the DA and that are also supported by {{site.data.keyword.cloud_notm}} projects are checked. Any extra controls that are not included in the list of supported {{site.data.keyword.compliance_short}} rules are not checked when you validate the configuration.
{: important}

1.  Deploy the configuration. After you validate your configuration, you can deploy it to your target account:

    1.  Review the input values and make any necessary changes.
    2.  Click **Deploy**. Deploying the DA can take a few minutes. You are notified when the deployment is successful.

2.  Review the outputs from the DA.

3.  Once the deployment is complete, you will begin to see {{site.data.keyword.Bluemix_notm}} data in your Cloudability instance in 24 hours.

4.  You can validate that the connection to {{site.data.keyword.Bluemix_notm}} was completed in Cloudability under Vendor Credentials at https://app.apptio.com/cloudability#/credentials/ibm

During the validation and deployment process, monitor the [needs attention items](/docs/secure-enterprise?topic=secure-enterprise-needs-attention-projects). The widget reflects any issue that occurs in your configurations.
{: remember}
