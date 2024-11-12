---

copyright:
  years: 2024
lastupdated: "2024-11-12"

keywords:

subcollection: track-spend-with-cloudability

---

{{site.data.keyword.attribute-definition-list}}



# Getting help and support for {{site.data.keyword.IBM_notm}} Cloudability Enablement
{: #help-and-support}

If you experience an issue or have questions about deploying {{site.data.keyword.IBM_notm}} Cloudability Enablement, you can use the following resources before you open a support case.
{: shortdesc}

* Review the [FAQs](#faqs) in the deployment guide.
* Review the [troubleshooting documentation](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-troubleshoot) to troubleshoot and resolve common issues.
* ![{{site.data.keyword.cloud_notm}} icon](../icons/ibm-cloud-16.svg "{{site.data.keyword.cloud_notm}} icon") Check the status of the {{site.data.keyword.cloud_notm}} platform and resources by going to the [Status page](https://cloud.ibm.com/status){: external}.
* ![GitHub icon](../icons/logo-github-16.svg "GitHub icon") Review the [GitHub issues](https://github.com/terraform-ibm-modules/terraform-ibm-apptio-cloudability-onboarding){: external} to see whether other users experienced the same problem.


If you still can't resolve the problem, you can open a support case. For more information, see [Creating support cases](/docs/get-support?topic=get-support-open-case). And, if you're looking to provide feedback, see [Submitting feedback](/docs/overview?topic=overview-feedback).

## Providing support case details
{: #support-case-details}

To ensure that the support team can start investigating your case to provide a timely resolution, you must include details from two logs from your failed deployment.


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

If you're having issues deploying the deployable architecture, include the name of the deployable architecture as it is appears in the catalog.

However, if you successfully deployed and are instead having an issue with a service in the deployable architecture, set that service as the product name in the case.
