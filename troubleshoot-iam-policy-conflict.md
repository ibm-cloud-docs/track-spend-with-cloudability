---

copyright:
  years: 2024
lastupdated: "2024-11-27"

keywords: question about {{site.data.keyword.IBM_notm}} Cloudability Enablement

subcollection: track-spend-with-cloudability

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I see a `policy_conflict_error` in the logs after deploying the Cloudability Enablement DA?
{: #troubleshoot-iam-policy-conflict}
{: troubleshoot}

The policy being created exists in the ibm cloud account before deployment. The existing policy may have been created by another run of the {{site.data.keyword.IBM_notm}} Cloudability Enablement DA or the Cloudability provided terraform.
{: shortdesc}

The deployment of the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture failed with a similar error message in the schematics logs:
{: tsSymptoms}

```log
Error: [ERROR] Error creating servicePolicy: The policy wasn't created because an access policy with identical attributes already exists. Please update the roles in the existing policy (07e58eb6-4c28-42aa-a1bc-22be0779dfd9), or update the one you're trying to assign to include a different attribute assignment. {
    "StatusCode": 409,
    "Headers": { .. },
    "Result": {
        "errors": [
            {
                "code": "policy_conflict_error",
                "details": {
                    "conflicts_with": {
                        "etag": "1-93709fda16a1fa934e8ac72dab1594fa",
                        "policy": {
                            "created_at": "2024-10-17T16:36:56.501Z",
                            "created_by_id": "iam-ServiceId-7187433c-241f-4c9a-8cda-10f25900f233",
                            "href": "https://iam.cloud.ibm.com/v1/policies/07e58eb6-4c28-42aa-a1bc-22be0779dfd9",
                            "id": "07e58eb6-4c28-42aa-a1bc-22be0779dfd9",
                            "last_modified_at": "2024-10-17T16:36:56.501Z",
                            "last_modified_by_id": "iam-ServiceId-7187433c-241f-4c9a-8cda-10f25900f233",
                            "resources": [
                                {
                                    "attributes": [
                                        {
                                            "name": "serviceName",
                                            "operator": "stringEquals",
                                            "value": "billing"
                                        },
                                        {
                                            "name": "accountId",
                                            "operator": "stringEquals",
                                            "value": "0bae863b1df44b9e99f58734da909ab9"
                                        }
                                    ]
                                }
                            ],
                            "roles": [
                                {
                                    "description": "As a viewer, you can view service instances, but you can't modify them.",
                                    "display_name": "Viewer",
                                    "role_id": "crn:v1:bluemix:public:iam::::role:Viewer"
                                }
                            ],
                            "state": "active",
                            "subjects": [
                                {
                                    "attributes": [
                                        {
                                            "name": "iam_id",
                                            "value": "iam-ServiceId-6bf7af4e-6f07-4894-ab72-ff539dfb951a"
                                        }
                                    ]
                                }
                            ],
                            "type": "access"
                        }
                    }
                },
                "message": "The policy wasn't created because an access policy with identical attributes already exists. Please update the roles in the existing policy (07e58eb6-4c28-42aa-a1bc-22be0779dfd9), or update the one you're trying to assign to include a different attribute assignment."
            }
        ],
        "status_code": 409,
        "trace": "7ac82ed5585d45d39d9cf853f8256135"
    },
    "RawResult": null
}
  with module.cloudability_enterprise_access[0].ibm_iam_service_policy.billing_policy[0],
  on modules/cloudability-enterprise-access/main.tf line 37, in resource "ibm_iam_service_policy" "billing_policy":
  37: resource "ibm_iam_service_policy" "billing_policy" {

severity: error
resource: ibm_iam_service_policy
operation: create
```
{: pre}

This error is due to the IAM policies that grant Cloudability access to the {{site.data.keyword.cos_short}} bucket existing in the IBM Cloud account.
{: tsCauses}

The recommended approach is to delete the existing policy and re-run the DA configuration to add the account. Deleting and re-creating the policy ensures that the vendor credentials within Cloudability are set correctly and managed by the project.
{: tsResolve}

These policies are not visible from the {{site.data.keyword.cloud_notm}} platform UI since the service ID exists in a different account. Instead, the policy needs to be deleted that uses the {{site.data.keyword.cloud_notm}} CLI or API. To delete the policy, use the following steps:

You need the `Administrator` role for `IAM Access Management` to be able to delete the policies.
{: important }

1. Log in to the {{site.data.keyword.cloud_notm}} [CLI](#x2051424){: term} and select the corresponding account where the policy conflict exists.
2. Retrieve the list of policy IDs, which are attached to the Cloudability Service ID. The following command can be used to extract the policy IDs (this command uses [curl](https://curl.se/) and [jq](https://github.com/jqlang/jq)).

    ```bash
    curl -X GET "https://iam.cloud.ibm.com/v1/policies?account_id=$(ibmcloud account show -o JSON | jq -r '.account_id')" -H "Authorization:$(ibmcloud iam oauth-tokens -o JSON | jq -r '.iam_token')" -H 'Content-Type: application/json' | jq '.policies[] | select(.subjects[].attributes[].value == "iam-ServiceId-6bf7af4e-6f07-4894-ab72-ff539dfb951a") | .id'
    ```
    {: pre}

3. Delete the policies granted to the Cloudability Service ID by issuing the following command and replacing `POLICY_ID` with the ID's from the output of the previous step.

    ```bash
    ibmcloud iam service-policy-delete ServiceId-6bf7af4e-6f07-4894-ab72-ff539dfb951a POLICY_ID
    ```
    {: pre}

4. [Redeploy the Cloudability DA](/docs/secure-enterprise?topic=secure-enterprise-deploy-project&interface=ui#deploy-config-copy) to re-create these policies.

The issue should be resolved and the policies re-created. If the issue continues, [open a case](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-help-and-support) in the {{site.data.keyword.cloud_notm}} support center.
