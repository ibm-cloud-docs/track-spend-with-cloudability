---

copyright:
  years: 2024
lastupdated: "2024-11-27"

keywords:

subcollection: track-spend-with-cloudability

---

{{site.data.keyword.attribute-definition-list}}



# Getting help and support for {{site.data.keyword.IBM_notm}} Cloudability Enablement
{: #help-and-support}

If you have any questions or experience an issue deploying or configuring the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture, then you can use the following resources before you open a support case. For support related to IBM Cloudability, visit the [Cloudability Help Center](https://help.apptio.com/en-us/cloudability/home.htm) or visit [IBM Support](https://www.ibm.com/mysupport/s/)
{: shortdesc}

* Review the [FAQs](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-ibm-cloud-enablement-faqs) in the deployment guide.
* Review the [troubleshooting documentation](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-ts-deploy-failed) to troubleshoot and resolve common issues.
* ![{{site.data.keyword.cloud_notm}} icon](../icons/ibm-cloud-16.svg "{{site.data.keyword.cloud_notm}} icon") Check the status of the {{site.data.keyword.cloud_notm}} platform and resources by going to the [Status page](https://cloud.ibm.com/status){: external}.
* ![GitHub icon](../icons/logo-github-16.svg "GitHub icon") Review the [GitHub issues](https://github.com/terraform-ibm-modules/terraform-ibm-cloudability-onboarding){: external} to see whether other users experienced the same problem.
* Review the [Cloudability documentation](https://help.apptio.com/en-us/cloudability/product/setup_ibm_cloud_credentials_using_da_method.htm){: external}
* Search [IBM Support](https://www.ibm.com/mysupport/s/){: external}

If you still can't resolve the problem, you can open a support case with IBM Cloud. For more information, see [Creating IBM Cloud support cases](/docs/account?topic=account-open-case&interface=ui). And, if you're looking to provide feedback, see [Submitting feedback](/docs/overview?topic=overview-feedback).

## Providing IBM Cloud support case details
{: #support-case-details}

For support with issues related to the use of IBM Cloudability, create a support case in [IBM Support](https://www.ibm.com/mysupport/s/){: external} rather than {{site.data.keyword.cloud_notm}}.
{: important}

To ensure that the IBM Cloud support team can start investigating your case to provide a timely resolution, you must include details from two logs from your failed deployment:


1. From your Schematics log, provide the architecture name, source URL, and version.

    a. In the {{site.data.keyword.cloud_notm}} console, go to `Schematics` > `Workspaces` > **deployable architecture instance**.

    b. Copy and paste into the case details the portion of the log that provides the architecture information. The following contents is an example of the case details which can be copied from the schematics logs:

      ```sh
      2023/04/06 18:11:43 Related Workspace: name=deploy-arch-ibm-cloudability-04-06-2023, sourcerelease=(not specified), sourceurl=https modules/terraform-ibm-cloudability-onboarding/archive/v1.0.3.tar.gz,tolder=terratorm-ibm-terraform-ibm-cloudability-onboarding-1.0.3/modules/roks
       ```

2. From your project, provide the Terraform Log Analyzer summary.
   a. In the {{site.data.keyword.cloud_notm}} console, go to **your project** > **Configurations** > **deployable architecture instance**.
   b. Depending on where you are in your deployment process go to `View validation results` or `View last deployment`. Take a screenshot of the results and add it to your support case.

## Routing your support case expeditiously
{: #support-case-routing}

To get your support case routed correctly to speed up resolution, make sure that you select the right product when you open the case.

If you're having issues deploying the deployable architecture, include the name of the deployable architecture as it appears in the catalog.

However, if you successfully deployed and are instead having an issue with a service in the deployable architecture, set that service as the product name in the case.

For technical support related to Cloudability, visit the [Cloudability help center](https://help.apptio.com/en-us/cloudability/home.htm){: external} or open a ticket with [IBM Support](https://www.ibm.com/mysupport/s/){: external}
