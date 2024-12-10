---

copyright:
  years: 2024
lastupdated: "2024-12-10"

keywords: question about {{site.data.keyword.IBM_notm}} Cloudability Enablement

subcollection: track-spend-with-cloudability

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do the iam custom roles fail to be created?
{: #troubleshoot-iam-role-conflict}
{: troubleshoot}

The iam custom roles with the same names and policies exist in the {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

The deployment of the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture failed with a similar error message in the schematics logs:
{: tsSymptoms}

```log
with module.cloudability_bucket_access.ibm_iam_custom_role.cos_custom_role[0],
   on modules/cloudability-bucket-access/main.tf line 18, in resource "ibm_iam_custom_role" "cos_custom_role":
    18: resource "ibm_iam_custom_role" "cos_custom_role" {

  ---
  id: terraform-a8d57e63
  summary: |
    [ERROR] Error creating Custom Roles: This role name has already been used, please update the existing one or change the role name.
    {
        "StatusCode": 409,
        "Headers": {...},
        "Result": {
            "errors": [
                {
                    "code": "role_conflict_error",
                    "details": {
                        "conflicts_with": {
                            "etag": "9-da505242e269012859dfe3c897ec83dd",
                            "role": {
                                "account_id": "0bae863b1df44b9e99f58734da909ab9",
                                "actions": [
                                    "iam.policy.read",
                                    "cloud-object-storage.object.head",
                                    "cloud-object-storage.object.get_uploads",
                                    "cloud-object-storage.object.get",
                                    "cloud-object-storage.bucket.list_bucket_crn",
                                    "cloud-object-storage.bucket.head",
                                    "cloud-object-storage.bucket.get"
                                ],
                                "created_at": "2024-10-17T16:36:56.161Z",
                                "created_by_id": "iam-ServiceId-7187433c-241f-4c9a-8cda-10f25900f233",
                                "crn": "crn:v1:ibmcloud:public:iam-access-management::a/0bae863b1df44b9e99f58734da909ab9::customRole:CloudabilityStorageCustomRole",
                                "description": "This is a custom role to read Cloud Storage",
                                "display_name": "CloudabilityStorageCustomRole",
                                "href": "https://iam.cloud.ibm.com/v2/roles/637573746f6d526f6c652d32636465636165313938663634316530616565643466313937323666643065332d436c6f75646162696c69747953746f72616765437573746f6d526f6c65",
                                "id": "637573746f6d526f6c652d32636465636165313938663634316530616565643466313937323666643065332d436c6f75646162696c69747953746f72616765437573746f6d526f6c65",
                                "last_modified_at": "2024-10-17T16:36:56.161Z",
                                "last_modified_by_id": "iam-ServiceId-7187433c-241f-4c9a-8cda-10f25900f233",
                                "name": "CloudabilityStorageCustomRole",
                                "service_name": "cloud-object-storage"
                            }
                        }
                    },
                    "message": "This role name has already been used, please update the existing one or change the role name."
                }
            ],
            "status_code": 409,
            "trace": "f65c2f3a4856496196adf3132dd8a90b"
        },
        "RawResult": null
    }
  severity: error
  resource: ibm_iam_custom_role
  operation: create
```
{: pre}


This error is often because the {{site.data.keyword.cloud_notm}} account contains custom roles by the same name and with the same policies. A separate deployment of the Cloudability deployable architecture or the Cloudability provided terraform script may have created these custom roles in the account.
{: tsCauses}


The recommended approach is to manually delete the iam custom roles from the [iam roles UI](/iam/roles) or by running the **Destroy resources** option within {{site.data.keyword.IBM}} Projects. Once destroyed, [re-run the Cloudability deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-deploy-project&interface=ui#deploy-config-copy) to re-create the custom iam roles under the current project.
{: tsResolve}
