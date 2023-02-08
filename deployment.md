Copyright 2022 Google LLC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

     http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.13 |
| <a name="requirement_google"></a> [google](#requirement\_google) | >= 3.50 |
| <a name="requirement_google-beta"></a> [google-beta](#requirement\_google-beta) | >= 3.50 |

## Providers

No providers.

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_cost_optimization"></a> [cost\_optimization](#module\_cost\_optimization) | ../../../modules/cost-optimization | n/a |

## Resources

No resources.

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_activate_apis"></a> [activate\_apis](#input\_activate\_apis) | The list of apis to activate within the project | `list(string)` | `[]` | no |
| <a name="input_asset_export_scheduler_job_config"></a> [asset\_export\_scheduler\_job\_config](#input\_asset\_export\_scheduler\_job\_config) | Asset Export Cloud Scheduler Job Config | <pre>object({<br>    schedule         = string,<br>    attempt_deadline = string,<br>    http_method      = string<br>  })</pre> | <pre>{<br>  "attempt_deadline": "1800s",<br>  "http_method": "GET",<br>  "schedule": "0 */1 * * *"<br>}</pre> | no |
| <a name="input_bq_org_asset_inventory_dataset"></a> [bq\_org\_asset\_inventory\_dataset](#input\_bq\_org\_asset\_inventory\_dataset) | BiqQuery Asset Inventory Dataset Name | `string` | n/a | yes |
| <a name="input_bq_utlization_dataset"></a> [bq\_utlization\_dataset](#input\_bq\_utlization\_dataset) | BiqQuery Utilization Dataset Name | `string` | n/a | yes |
| <a name="input_cloud_run_config"></a> [cloud\_run\_config](#input\_cloud\_run\_config) | Cloud Run Configuration | <pre>object({<br>    service_name          = string,<br>    timeout_seconds       = number,<br>    container_concurrency = number,<br>    limits                = map(string),<br>    template_annotations  = map(string)<br>  })</pre> | <pre>{<br>  "container_concurrency": 10,<br>  "limits": {<br>    "cpu": "1000m",<br>    "memory": "1024M"<br>  },<br>  "service_name": "utilization-export",<br>  "template_annotations": {<br>    "autoscaling.knative.dev/maxScale": "200"<br>  },<br>  "timeout_seconds": 1800<br>}</pre> | no |
| <a name="input_cloudrun_image_version"></a> [cloudrun\_image\_version](#input\_cloudrun\_image\_version) | Cloud Run Image Version | `string` | n/a | yes |
| <a name="input_config_tmpl_name"></a> [config\_tmpl\_name](#input\_config\_tmpl\_name) | Config Template File Name | `string` | `"config.yaml.tmpl"` | no |
| <a name="input_create_cloudrun_sa"></a> [create\_cloudrun\_sa](#input\_create\_cloudrun\_sa) | Set to true if you want to create service account for Cloud Run | `bool` | `true` | no |
| <a name="input_default_app_engine_location"></a> [default\_app\_engine\_location](#input\_default\_app\_engine\_location) | Default App Engine Location | `string` | `"us-central"` | no |
| <a name="input_enable_apis"></a> [enable\_apis](#input\_enable\_apis) | Set to true if you want to enable service APIs | `bool` | `true` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | Environment Name | `string` | n/a | yes |
| <a name="input_location"></a> [location](#input\_location) | Location to create BigQuery Dataset | `string` | `"US"` | no |
| <a name="input_mql_time_window"></a> [mql\_time\_window](#input\_mql\_time\_window) | MQL Time Window | `string` | `"1h"` | no |
| <a name="input_organization_id"></a> [organization\_id](#input\_organization\_id) | Organization ID | `string` | n/a | yes |
| <a name="input_project_id"></a> [project\_id](#input\_project\_id) | Project ID where all this will be setup . | `string` | n/a | yes |
| <a name="input_pubsub_topics"></a> [pubsub\_topics](#input\_pubsub\_topics) | List of Pub/Sub Topics | `list(string)` | <pre>[<br>  "metrics",<br>  "dead-letter",<br>  "bigquery"<br>]</pre> | no |
| <a name="input_region"></a> [region](#input\_region) | Region Name | `string` | n/a | yes |
| <a name="input_service_account"></a> [service\_account](#input\_service\_account) | Existing Service Account for Cloud Run. Provide only if you not create service account by setting create\_cloudrun\_sa to false | `string` | `""` | no |
| <a name="input_service_account_name"></a> [service\_account\_name](#input\_service\_account\_name) | Service Account Name for Cloud Run | `string` | `""` | no |
| <a name="input_utilization_scheduler_job_config"></a> [utilization\_scheduler\_job\_config](#input\_utilization\_scheduler\_job\_config) | Utilization Cloud Scheduler Job Config | <pre>object({<br>    schedule         = string,<br>    attempt_deadline = string,<br>    http_method      = string<br>  })</pre> | <pre>{<br>  "attempt_deadline": "1800s",<br>  "http_method": "GET",<br>  "schedule": "0 */1 * * *"<br>}</pre> | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_bigquery_asset_inventory_dataset"></a> [bigquery\_asset\_inventory\_dataset](#output\_bigquery\_asset\_inventory\_dataset) | BigQuery Org Asset Inventory Dataset |
| <a name="output_bigquery_subscription_id"></a> [bigquery\_subscription\_id](#output\_bigquery\_subscription\_id) | BigQuery Pub/Sub Subscription ID |
| <a name="output_bigquery_utilization_dataset"></a> [bigquery\_utilization\_dataset](#output\_bigquery\_utilization\_dataset) | BigQuery Utilization Dataset |
| <a name="output_bigquery_utlization_tables"></a> [bigquery\_utlization\_tables](#output\_bigquery\_utlization\_tables) | BigQuery Utilization Tables |
| <a name="output_cloudrun_revision"></a> [cloudrun\_revision](#output\_cloudrun\_revision) | Cloud Run Service Revision |
| <a name="output_cloudrun_service_name"></a> [cloudrun\_service\_name](#output\_cloudrun\_service\_name) | Cloud Run Service Name |
| <a name="output_cloudrun_service_status"></a> [cloudrun\_service\_status](#output\_cloudrun\_service\_status) | Cloud Run Service Status |
| <a name="output_cloudrun_service_url"></a> [cloudrun\_service\_url](#output\_cloudrun\_service\_url) | Cloud Run Service URL |
| <a name="output_enabled_apis"></a> [enabled\_apis](#output\_enabled\_apis) | List of APIs Enabled |
| <a name="output_metrics_subscription_id"></a> [metrics\_subscription\_id](#output\_metrics\_subscription\_id) | Metrics Pub/Sub Subscription ID |
| <a name="output_pubsub_topics"></a> [pubsub\_topics](#output\_pubsub\_topics) | Pub/Sub Topics |
| <a name="output_tables_list"></a> [tables\_list](#output\_tables\_list) | List of BigQuery Tables |
| <a name="output_views_list"></a> [views\_list](#output\_views\_list) | List of BigQuery Views |
