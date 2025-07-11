# Active Directory Entity Analytics

This Active Directory Entity Analytics integration allows users to securely stream User Entities data to Elastic Security via the Active Directory LDAP look-ups. When integrated with Elastic Security, this valuable data can be leveraged within Elastic for risk-scoring scenarios (e.g., context enrichments) and detecting advanced analytics (UBA) use cases.

## Data streams

The Active Directory Entity Analytics integration collects one type of data: user.

- **User** is used to retrieve all user entries available from an Active Directory server.

## Requirements

Elastic Agent must be installed. For more details, check the Elastic Agent [installation instructions](docs-content://reference/fleet/install-elastic-agents.md).

## Setup

### Collect data from Active Directory

1. Obtain the LDAP username, for example `CN=Administrator,CN=Users,DC=testserver,DC=local` and password, and LDAP host address for the Active Directory server that you will be collecting data from.
2. Determine the Base DN for the directory to be used, for example `CN=Users,DC=testserver,DC=local`.

### Enabling the integration in Elastic:

1. In Kibana navigate to **Management** > **Integrations**.
2. In the search bar, type **Active Directory Entity Analytics**.
3. Select the **Active Directory Entity Analytics** integration and add it.
4. While adding the integration, add the user, host and base DN details obtained above.
5. Save the integration.

## Usage

The Active Directory provider periodically contacts the server, retrieving updates for users, updates its internal cache of user metadata, and ships updated user metadata to Elasticsearch.

Fetching and shipping updates occurs in one of two processes: **full synchronizations** and **incremental updates**. Full synchronizations will send the entire list of users in state, along with write markers to indicate the start and end of the synchronization event. Incremental updates will only send data for changed users during that event. Changes on a user can come in many forms, whether it be a change to the user’s metadata, or a user was added or deleted. By default, full synchronizations occur every 24 hours and incremental updates occur every 15 minutes. These intervals may be customized to suit your use case.

## Logs reference

### User

This is the `User` dataset.

#### Example

An example event for `user` looks as following:

```json
{
    "@timestamp": "2024-04-02T02:44:08.198Z",
    "agent": {
        "ephemeral_id": "c8f2cffa-8316-41a2-8ad6-89ef2f3ecd2b",
        "id": "277a9e26-8aae-4bc6-abcc-21db22ad29d7",
        "name": "docker-fleet-agent",
        "type": "filebeat",
        "version": "8.13.0"
    },
    "asset": {
        "category": "entity",
        "type": "activedirectory_user"
    },
    "data_stream": {
        "dataset": "entityanalytics_ad.user",
        "namespace": "ep",
        "type": "logs"
    },
    "ecs": {
        "version": "8.17.0"
    },
    "elastic_agent": {
        "id": "277a9e26-8aae-4bc6-abcc-21db22ad29d7",
        "snapshot": false,
        "version": "8.13.0"
    },
    "event": {
        "action": "started",
        "agent_id_status": "verified",
        "category": [
            "iam"
        ],
        "dataset": "entityanalytics_ad.user",
        "ingested": "2024-04-02T02:44:20Z",
        "kind": "asset",
        "start": "2024-04-02T02:44:08.198Z",
        "type": [
            "info"
        ]
    },
    "input": {
        "type": "entity-analytics"
    },
    "labels": {
        "identity_source": "entity-analytics-entityanalytics_ad.user-2270bd23-5392-4185-959b-b01ac2b8d89a"
    },
    "tags": [
        "users-entities",
        "preserve_duplicate_custom_fields",
        "forwarded",
        "entityanalytics_ad-user"
    ]
}
```

**Exported fields**

| Field | Description | Type |
|---|---|---|
| @timestamp | Event timestamp. | date |
| asset.category |  | keyword |
| asset.costCenter |  | keyword |
| asset.create_date |  | date |
| asset.id |  | keyword |
| asset.last_seen |  | date |
| asset.last_status_change_date |  | date |
| asset.last_updated |  | date |
| asset.name |  | keyword |
| asset.status |  | keyword |
| asset.type |  | keyword |
| asset.vendor |  | keyword |
| data_stream.dataset | Data stream dataset. | constant_keyword |
| data_stream.namespace | Data stream namespace. | constant_keyword |
| data_stream.type | Data stream type. | constant_keyword |
| entityanalytics_ad.groups.admin_count |  | keyword |
| entityanalytics_ad.groups.cn |  | keyword |
| entityanalytics_ad.groups.description |  | keyword |
| entityanalytics_ad.groups.distinguished_name |  | keyword |
| entityanalytics_ad.groups.ds_core_propagation_data |  | date |
| entityanalytics_ad.groups.group_type |  | keyword |
| entityanalytics_ad.groups.id |  | keyword |
| entityanalytics_ad.groups.instance_type |  | keyword |
| entityanalytics_ad.groups.is_critical_system_object |  | boolean |
| entityanalytics_ad.groups.member |  | keyword |
| entityanalytics_ad.groups.member_of |  | keyword |
| entityanalytics_ad.groups.name |  | keyword |
| entityanalytics_ad.groups.object_category |  | keyword |
| entityanalytics_ad.groups.object_class |  | keyword |
| entityanalytics_ad.groups.object_guid |  | keyword |
| entityanalytics_ad.groups.object_sid |  | keyword |
| entityanalytics_ad.groups.sam_account_name |  | keyword |
| entityanalytics_ad.groups.sam_account_type |  | keyword |
| entityanalytics_ad.groups.usn_changed |  | keyword |
| entityanalytics_ad.groups.usn_created |  | keyword |
| entityanalytics_ad.groups.when_changed |  | date |
| entityanalytics_ad.groups.when_created |  | date |
| entityanalytics_ad.id |  | keyword |
| entityanalytics_ad.user.account_expires |  | keyword |
| entityanalytics_ad.user.account_never_expires | True if the account is set to never expire. | boolean |
| entityanalytics_ad.user.admin_count |  | keyword |
| entityanalytics_ad.user.bad_password_time |  | keyword |
| entityanalytics_ad.user.bad_pwd_count |  | keyword |
| entityanalytics_ad.user.cn |  | keyword |
| entityanalytics_ad.user.code_page |  | keyword |
| entityanalytics_ad.user.constrained_delegation | True if the account is trusted for constrained delegation. | boolean |
| entityanalytics_ad.user.country_code |  | keyword |
| entityanalytics_ad.user.description |  | keyword |
| entityanalytics_ad.user.distinguished_name |  | keyword |
| entityanalytics_ad.user.dont_require_preauth | True if the account does not require Kerberos pre-authentication. | boolean |
| entityanalytics_ad.user.ds_core_propagation_data |  | date |
| entityanalytics_ad.user.enabled | If the account is enabled. | boolean |
| entityanalytics_ad.user.instance_type |  | keyword |
| entityanalytics_ad.user.is_critical_system_object |  | boolean |
| entityanalytics_ad.user.last_logoff |  | keyword |
| entityanalytics_ad.user.last_logon |  | date |
| entityanalytics_ad.user.last_logon_timestamp |  | date |
| entityanalytics_ad.user.locked | True if the account is locked out. | boolean |
| entityanalytics_ad.user.logon_count |  | keyword |
| entityanalytics_ad.user.logon_script_enabled | True if a logon script is configured for the account. | boolean |
| entityanalytics_ad.user.member_of |  | keyword |
| entityanalytics_ad.user.msDS-\* |  | keyword |
| entityanalytics_ad.user.name |  | keyword |
| entityanalytics_ad.user.object_category |  | keyword |
| entityanalytics_ad.user.object_class |  | keyword |
| entityanalytics_ad.user.object_dn |  | keyword |
| entityanalytics_ad.user.object_guid |  | keyword |
| entityanalytics_ad.user.object_sid |  | keyword |
| entityanalytics_ad.user.password_not_required | True if the account does not require a password. | boolean |
| entityanalytics_ad.user.primary_group_id |  | keyword |
| entityanalytics_ad.user.privileged_group_member | True if the user is a member of a privileged group. | boolean |
| entityanalytics_ad.user.pwd_last_set |  | date |
| entityanalytics_ad.user.reversible_encryption_password | True if the user password is stored with reversible encryption. | boolean |
| entityanalytics_ad.user.sam_account_name |  | keyword |
| entityanalytics_ad.user.sam_account_type |  | keyword |
| entityanalytics_ad.user.sensitive_object | True if the account cannot be delegated. | boolean |
| entityanalytics_ad.user.service_principal_name |  | keyword |
| entityanalytics_ad.user.show_in_advanced_view_only |  | boolean |
| entityanalytics_ad.user.uac_list |  | keyword |
| entityanalytics_ad.user.unconstrained_delegation | True if the account is trusted for unconstrained delegation. | boolean |
| entityanalytics_ad.user.use_des_key_only | True if the account is configured to only use DES encryption. | boolean |
| entityanalytics_ad.user.user_account_control |  | keyword |
| entityanalytics_ad.user.usn_changed |  | keyword |
| entityanalytics_ad.user.usn_created |  | keyword |
| entityanalytics_ad.user.when_changed |  | date |
| entityanalytics_ad.user.when_created |  | date |
| entityanalytics_ad.when_changed |  | date |
| event.dataset | Event dataset. | constant_keyword |
| event.module | Event module. | constant_keyword |
| input.type | Type of filebeat input. | keyword |
| labels.identity_source |  | keyword |
| user.account.activated_date |  | date |
| user.account.change_date |  | date |
| user.account.create_date |  | date |
| user.account.password_change_date |  | date |
| user.account.status.deprovisioned |  | boolean |
| user.account.status.locked_out |  | boolean |
| user.account.status.password_expired |  | boolean |
| user.account.status.recovery |  | boolean |
| user.account.status.suspended |  | boolean |
| user.geo.city_name |  | keyword |
| user.geo.country_iso_code |  | keyword |
| user.geo.name |  | keyword |
| user.geo.postal_code |  | keyword |
| user.geo.region_name |  | keyword |
| user.geo.timezone |  | keyword |
| user.organization.name |  | keyword |
| user.profile.department |  | keyword |
| user.profile.first_name |  | keyword |
| user.profile.id |  | keyword |
| user.profile.job_title |  | keyword |
| user.profile.last_name |  | keyword |
| user.profile.manager |  | keyword |
| user.profile.mobile_phone |  | keyword |
| user.profile.other_identities |  | keyword |
| user.profile.primaryPhone |  | keyword |
| user.profile.secondEmail |  | keyword |
| user.profile.status |  | keyword |
| user.profile.type |  | keyword |

