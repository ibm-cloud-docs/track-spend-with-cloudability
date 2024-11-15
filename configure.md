---

copyright:
  years: 2024
lastupdated: "2024-11-15"

keywords:

subcollection: track-spend-with-cloudability

---

{{site.data.keyword.attribute-definition-list}}

# Configuration reference for {{site.data.keyword.IBM_notm}} Cloudability enablement
{: #configure}

The {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture (DA) requires two parameters to run:

1.  An {{site.data.keyword.cloud_notm}} IAM API key with permissions to run the deployable architecture
2.  An {{site.data.keyword.IBM_notm}} Cloudability API Key to add the {{site.data.keyword.cloud_notm}} Account to Cloudability

See [setting up the {{site.data.keyword.IBM_notm}} Cloudability Enablement DA](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning) for information about these parameters and how to create them.

Use this guide as a configuration reference to customize your DA deployment.

## Supported regions
{: #regions}

The DA supports deployment to any of the available [{{site.data.keyword.keymanagementserviceshort}} regions](/docs/key-protect?topic=key-protect-regions). Your {{site.data.keyword.keymanagementserviceshort}} instance and {{site.data.keyword.cos_short}} bucket are created in the same region. The default region is `us-south`.

It is recommended to use one of the three [{{site.data.keyword.keymanagementserviceshort}} failover regions](/docs/key-protect?topic=key-protect-ha-dr#availability) (us-south, jp-tok, and eu-de) to avoid any service disruptions.
{: recommend }



## Configuration options
{: #configuration-options}

### Enterprise accounts
{: #enterprise-account-inputs}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `is_enterprise_account` | Whether the account being added to Cloudability is the primary account within an enterprise. The `ibmcloud_api_key` should be created within the primary enterprise account | `bool` | `false` |
| `enterprise_id` | The ID of the enterprise. If `__NULL__` then it is automatically retrieved if `is_enterprise_account` is `true`. Providing this value reduces the access policies that are required to run the DA. | `string` | `__NULL__` |
{: caption="Table 1. Enterprise Account Parameters" caption-side="bottom"}

### {{site.data.keyword.IBM_notm}} Cloudability configurations
{: #cloudability-config}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `cloudability_host` | {{site.data.keyword.IBM_notm}} Cloudability host name as described in https://help.apptio.com/en-us/cloudability/api/v3/getting_started_with_the_cloudability.htm#authentication | `string` | `"api.cloudability.com"` |
| `skip_verification` | Whether to verify the account after the account is added to Cloudability. This step is not strictly necessary for adding the account to Cloudability | `bool` | `false` |
{: caption="Table 2. {{site.data.keyword.IBM_notm}} Cloudability Configurations" caption-side="bottom"}


### {{site.data.keyword.cloud_notm}} resource group
{: #resource-group-config}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `use_existing_resource_group` | Whether the value of `resource_group_name` input should be a new or an existing resource group | `bool` | `true` |
| `resource_group_name` | The name of a new or existing resource group where resources will be created | `string` | `"Default"` |
{: caption="Table 3. Resource Group" caption-side="bottom"}

### Tagging
{: #tagging}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `access_tags` | List of access tags to be added to created resources | list of `string` | `[]` |
| `resource_tags` | List of tags to be added to created resources" | list of `string` | `[]` |
{: caption="Table 4. Tagging" caption-side="bottom"}


### Billing exports
{: #billing-exports-config}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `overwrite_existing_reports` | Whether each update overwrites the existing report version or a new version of the report is created leaving the existing report | `bool` | `true` |
| `cos_folder` | Folder or prefix in the {{site.data.keyword.cos_short}} bucket to store the billing reports | `string` | `"IBMCloud-Billing-Reports"` |
{: caption="Table 5. Billing Exports" caption-side="bottom"}


### {{site.data.keyword.cos_full_notm}} bucket
{: #cos-billing-exports-config}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `existing_cos_instance_id` | The ID of an existing {{site.data.keyword.cos_full_notm}} instance. | `string` | `__NULL__` |
| `cos_instance_name` | The name of the newly created {{site.data.keyword.cos_full_notm}} instance which contains the billing reports bucket. Only used if `existing_cos_instance_id` is not defined. | `string` | `"ibm-cloudability"` |
| `bucket_name` | Name to the {{site.data.keyword.cos_short}} bucket where billing reports are stored. | `string` | `"apptio-cldy-billing-snapshots"` |
| `add_bucket_name_suffix`. | Add a random 4 character suffix to the `bucket_name` to ensure global uniqueness. | `bool` | `true` |
| `cos_plan` | Plan to be used for creating {{site.data.keyword.cos_full_notm}} instance. Only used if `existing_cos_instance_id` is not defined. | `string` | `"One Rate"` |
| `bucket_storage_class` | The storage class of the newly provisioned {{site.data.keyword.cos_short}} bucket. | `string` | `"standard"` |
| `expire_days` | Specifies the number of days when the expired rule action takes effect. Value of `__NULL__` disables expiry. [Learn more about object expiration](/docs/cloud-object-storage?topic=cloud-object-storage-expiry) | `number` | `3` |
| `object_versioning_enabled` | Enable object versioning to keep multiple versions of an object in the object storage bucket | `bool` | `false` |
| `archive_days` | Specifies the number of days when the archive rule action takes effect. Value of `__NULL__` disables archiving | `number` | `__NULL__` |
| `archive_type` | Specifies the storage class or archive type to which you want the object to transition. | `string` | `"Glacier"` |
{: caption="Table 6. {{site.data.keyword.cos_full_notm}} Bucket" caption-side="bottom"}

### {{site.data.keyword.cos_short}} bucket encryption with {{site.data.keyword.keymanagementserviceshort}}
{: #cos-bucket-encryption-config}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `existing_kms_instance_guid` | The GUID of the {{site.data.keyword.keymanagementserviceshort}} instance. | `string` | `__NULL__` |
| `key_protect_instance_name` | Name of the {{site.data.keyword.keymanagementserviceshort}} instance name used for bucket encryption | `string` | `"cloudability-bucket-encryption"` |
| `key_ring_name` | Name of the key ring to group keys | `string` | `"bucket-encryption"` |
| `key_name` | Name of the encryption key for the Object Storage bucket | `string` | `cldy-bucket-key` |
{: caption="Table 7. Bucket Encryption with {{site.data.keyword.keymanagementserviceshort}}" caption-side="bottom"}

### Bucket audit events
{: #bucket-audit-events}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `activity_tracker_read_data_events` | If set to `true`, all {{site.data.keyword.cos_short}} bucket read events are sent to Activity Tracker. | `boolean` | `true` |
| `activity_tracker_write_data_events` | If set to `true`, all {{site.data.keyword.cos_short}} bucket write events are sent to Activity Tracker. | `boolean` | `true` |
| `activity_tracker_management_events` | If set to `true`, all {{site.data.keyword.cos_short}} management events are sent to Activity Tracker. | `boolean` | `true` |
{: caption="Table 8. Bucket audit events" caption-side="bottom"}

### Bucket metrics
{: #bucket-metrics}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `monitoring_crn` | The CRN of an {{site.data.keyword.cloud_notm}} Monitoring instance where {{site.data.keyword.cos_short}} bucket metrics are sent. If no value is passed, metrics are sent to the instance associated with the Metrics Router service configuration. | `string` | `__NULL__` |
| `request_metrics_enabled` | If set to `true`, all {{site.data.keyword.cos_short}} bucket request metrics will be sent to the monitoring service. | `boolean` | `true` |
| `usage_metrics_enabled` | If set to `true`, all {{site.data.keyword.cos_short}} bucket usage metrics will be sent to the monitoring service. | `boolean` | `true` |
{: caption="Table 8. Bucket metrics" caption-side="bottom"}

### IAM inputs
{: #iam-inputs}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `cloudability_custom_role_name` | name of the custom role, that is used to grant the Cloudability service ID read access to the billing reports within the Object Storage bucket | `string` | `"CloudabilityStorageCustomRole"` |
| `cloudability_enterprise_custom_role_name` | name of the custom role to grant access to a Cloudability service ID to read the enterprise information. Only used of `is_enterprise_account` is set. | `string` | `"CloudabilityListAccCustomRole"` |
{: caption="Table 9. IAM inputs" caption-side="bottom"}
