---

copyright:
  years: 2025
lastupdated: "2025-01-09"

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

## Supported regions
{: #regions}

The DA supports deployment to any of the available [{{site.data.keyword.keymanagementserviceshort}} regions](/docs/key-protect?topic=key-protect-regions). Your {{site.data.keyword.keymanagementserviceshort}} instance and {{site.data.keyword.cos_short}} bucket are created in the same region. The default region is `us-south`.

{{site.data.keyword.cloud_notm}} recommends using one of the three [{{site.data.keyword.keymanagementserviceshort}} failover regions](/docs/key-protect?topic=key-protect-ha-dr#availability) (us-south, jp-tok, and eu-de) to avoid any service disruptions.
{: recommend }

## Configuration options
{: #configuration-options}

### Enterprise accounts
{: #enterprise-account-inputs}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `is_enterprise_account` | Whether the account corresponding to the `ibmcloud_api_key` is an enterprise account and, if so, is the primary account within the enterprise. | `bool` | `false` |
| `enterprise_id` | The ID of the enterprise. If `__NULL__` then it is automatically retrieved if `is_enterprise_account` is `true`. Providing this value reduces the access policies that are necessary to run the DA. | `string` | `__NULL__` |
{: caption="Enterprise Account Parameters" caption-side="bottom"}

### {{site.data.keyword.IBM_notm}} Cloudability configurations
{: #cloudability-config}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `cloudability_auth_type` | Select Cloudability authentication mode. Options are:\n\n* `none`: no connection to Cloudability\n* `manual`: manually enter in the credentials in the Cloudability UI\n* `api_key`: use Cloudability API Keys\n* `frontdoor`: Frontdoor Access Administration | `string` | `none` |
| `cloudability_api_key` | Cloudability API Key used to authenticate with Cloudability to add the IBM Cloud account to the Cloudability environment. See [how to retrieve your Cloudability API key](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning#api-key) or visit the [Cloudability preferences page](https://app.apptio.com/cloudability#/settings/preferences). Required if `cloudability_auth_type` is set to `api_key`. | `string` | `__NULL__` |
| `frontdoor_public_key` | The public key that is used along with the `frontdoor_secret_key` to authenticate requests to Cloudability. Only required if `cloudability_auth_type` is `frontdoor`. See [acquiring an Access Administration API key](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning#frontdoor-api-key) for steps to create your credentials. | `string` | `__NULL__` |
| `frontdoor_secret_key` | The secret key that is used along with the `frontdoor_public_key` to authenticate requests to Cloudability. Only required if `cloudability_auth_type` is `frontdoor`.  See [acquiring an Access Administration API key](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning#frontdoor-api-key) for steps to create your credentials. | `string` | `__NULL__` |
| `cloudability_environment_id` | An ID corresponding to the Cloudability environment. Only required if `cloudability_auth_type` is `frontdoor`. | `string` | `__NULL__` |
| `cloudability_host` | {{site.data.keyword.IBM_notm}} Cloudability host name as described in (https://help.apptio.com/en-us/cloudability/api/v3/getting%20started%20with%20the%20cloudability.htm) | `string` | `api.cloudability.com` |
| `skip_verification` | Whether to verify that the {{site.data.keyword.cloud_notm}} account is successfully integrated with Cloudability. This step is not strictly necessary for adding the account to Cloudability. Only applicable when `cloudability_auth_type` is `api_key`. | `bool` | `false` |
{: caption="{{site.data.keyword.IBM_notm}} Cloudability Configurations" caption-side="bottom"}


### {{site.data.keyword.cloud_notm}} resource group
{: #resource-group-config}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `use_existing_resource_group` | Whether the value of `resource_group_name` input is a new (true) or an existing (false) resource group | `bool` | `false` |
| `resource_group_name` | The name of a new or existing resource group where resources are created | `string` | `cloudability-enablement` |
{: caption="Resource Group" caption-side="bottom"}

### Tagging
{: #tagging}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `access_tags` | List of access tags to be added to created resources | list of `string` | `[]` |
| `resource_tags` | List of tags to be added to created resources" | list of `string` | `[]` |
{: caption="Tagging" caption-side="bottom"}


### Billing exports
{: #billing-exports-config}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `overwrite_existing_reports` | Whether each update overwrites the existing report version or a new version of the report is created leaving the existing report | `bool` | `true` |
| `cos_folder` | Folder or prefix in the {{site.data.keyword.cos_short}} bucket to store the billing reports | `string` | `IBMCloud-Billing-Reports` |
{: caption="Billing Exports" caption-side="bottom"}


### {{site.data.keyword.cos_full_notm}} bucket
{: #cos-billing-exports-config}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `existing_cos_instance_id` | The ID of an existing {{site.data.keyword.cos_full_notm}} instance. | `string` | `__NULL__` |
| `cos_instance_name` | The name of the newly created {{site.data.keyword.cos_full_notm}} instance, which contains the billing reports bucket. Only used if `existing_cos_instance_id` is not defined. | `string` | `billing-report-exports` |
| `bucket_name` | Name to the {{site.data.keyword.cos_short}} bucket where billing reports are stored. | `string` | `billing-reports` |
| `add_bucket_name_suffix`. | Add a random 4 character suffix to the `bucket_name` to ensure global uniqueness. | `bool` | `true` |
| `cos_plan` | Plan to be used for creating {{site.data.keyword.cos_full_notm}} instance. Only used if `existing_cos_instance_id` is not defined. | `string` | `One Rate` |
| `bucket_storage_class` | The storage class of the newly provisioned {{site.data.keyword.cos_short}} bucket. | `string` | `standard` |
| `expire_days` | Specifies the number of days when the expired rule action takes effect. Value of `__NULL__` disables expiry. [Learn more about object expiration](/docs/cloud-object-storage?topic=cloud-object-storage-expiry) | `number` | `3` |
| `object_versioning_enabled` | Enable object versioning to keep multiple versions of an object in the object storage bucket | `bool` | `false` |
| `archive_days` | Specifies the number of days when the archive rule action takes effect. Value of `__NULL__` disables archiving | `number` | `__NULL__` |
| `archive_type` | Specifies the storage class or archive type to which you want the object to transition. | `string` | `Glacier` |
{: caption="{{site.data.keyword.cos_full_notm}} Bucket" caption-side="bottom"}

### {{site.data.keyword.cos_short}} bucket encryption with {{site.data.keyword.keymanagementserviceshort}}
{: #cos-bucket-encryption-config}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `existing_kms_instance_guid` | The GUID of the {{site.data.keyword.keymanagementserviceshort}} instance. | `string` | `__NULL__` |
| `skip_iam_authorization_policy` | Whether to skip the creation of an IAM authorization policy that permits the Object Storage instance to read the encryption key from the {{site.data.keyword.keymanagementserviceshort}} instance. WARNING: An authorization policy must exist before an encrypted bucket can be created. | `boolean` | `false` |
| `key_protect_instance_name` | Name of the {{site.data.keyword.keymanagementserviceshort}} instance, which stores the Object Storage encryption key. Not needed if `existing_kms_instance_guid` is used. | `string` | `cloudability-bucket-encryption` |
| `key_ring_name` | Name of the {{site.data.keyword.keymanagementserviceshort}} key ring to store the Object Storage encryption key. | `string` | `bucket-encryption` |
| `use_existing_key_ring` | Whether the `key_ring_name` corresponds to an existing key ring or a new key ring for storing the encryption key. | `boolean` | `false` |
| `key_name` | Name of the {{site.data.keyword.keymanagementserviceshort}} key for encryption of the Object Storage bucket. If `__NULL__` then the name of the Object Storage bucket is used instead. | `string` | `__NULL__` |
| `kms_rotation_enabled` | If set to true, {{site.data.keyword.keymanagementserviceshort}} enables a rotation policy on the {{site.data.keyword.keymanagementserviceshort}} instance. Only used if 'create_key_protect_instance' is true. | `boolean` | `false` |
| `kms_rotation_interval_month` | Specifies the number of months for the encryption key to be rotated.. Must be between 1 and 12 inclusive. | `number` | `1` |
{: caption="Bucket Encryption with {{site.data.keyword.keymanagementserviceshort}}" caption-side="bottom"}

### Bucket audit events
{: #bucket-audit-events}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `activity_tracker_read_data_events` | If set to `true`, all {{site.data.keyword.cos_short}} bucket read events are sent to Activity Tracker. | `boolean` | `true` |
| `activity_tracker_write_data_events` | If set to `true`, all {{site.data.keyword.cos_short}} bucket write events are sent to Activity Tracker. | `boolean` | `true` |
| `activity_tracker_management_events` | If set to `true`, all {{site.data.keyword.cos_short}} management events are sent to Activity Tracker. | `boolean` | `true` |
{: caption="Bucket audit events" caption-side="bottom"}

### Bucket metrics
{: #bucket-metrics}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `monitoring_crn` | The CRN of an {{site.data.keyword.mon_short}} instance where {{site.data.keyword.cos_short}} bucket metrics are sent. If no value is passed, metrics are sent to the instance associated with the Metrics Router service configuration. | `string` | `__NULL__` |
| `request_metrics_enabled` | If set to `true`, all {{site.data.keyword.cos_short}} bucket request metrics are sent to the monitoring service. | `boolean` | `true` |
| `usage_metrics_enabled` | If set to `true`, all {{site.data.keyword.cos_short}} bucket usage metrics are sent to the monitoring service. | `boolean` | `true` |
{: caption="Bucket metrics" caption-side="bottom"}

### IAM inputs
{: #iam-inputs}

| Name | Description | Type | Default |
|------|-------------|------|---------|
| `cloudability_iam_custom_role_name` | name of the custom role that is used to grant the Cloudability service ID read access to the billing reports within the Object Storage bucket | `string` | `CloudabilityStorageCustomRole` |
| `cloudability_iam_enterprise_custom_role_name` | name of the custom role to grant access to a Cloudability service ID to read the enterprise information. Only used of `is_enterprise_account` is set. | `string` | `CloudabilityListAccCustomRole` |
{: caption="IAM inputs" caption-side="bottom"}
