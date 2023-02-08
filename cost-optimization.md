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

| Name | Version |
|------|---------|
| <a name="provider_google"></a> [google](#provider\_google) | >= 3.50 |
| <a name="provider_local"></a> [local](#provider\_local) | n/a |
| <a name="provider_null"></a> [null](#provider\_null) | n/a |
| <a name="provider_template"></a> [template](#provider\_template) | n/a |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_bq_org_asset_inventory_dataset"></a> [bq\_org\_asset\_inventory\_dataset](#module\_bq\_org\_asset\_inventory\_dataset) | terraform-google-modules/bigquery/google | ~> 5.4 |
| <a name="module_bq_utilization"></a> [bq\_utilization](#module\_bq\_utilization) | terraform-google-modules/bigquery/google | ~> 5.4 |
| <a name="module_cloud_run"></a> [cloud\_run](#module\_cloud\_run) | GoogleCloudPlatform/cloud-run/google | ~> 0.2.0 |
| <a name="module_cloudrun_sa_project_level"></a> [cloudrun\_sa\_project\_level](#module\_cloudrun\_sa\_project\_level) | terraform-google-modules/service-accounts/google | ~> 4.1.1 |
| <a name="module_gcloud"></a> [gcloud](#module\_gcloud) | terraform-google-modules/gcloud/google | ~> 2.0 |
| <a name="module_project_services"></a> [project\_services](#module\_project\_services) | terraform-google-modules/project-factory/google//modules/project_services | ~> 14.1 |

## Resources

| Name | Type |
|------|------|
| [google_app_engine_application.app](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/app_engine_application) | resource |
| [google_bigquery_data_transfer_config.instance_scheduled_query](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_data_transfer_config) | resource |
| [google_bigquery_data_transfer_config.project_scheduled_query](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_data_transfer_config) | resource |
| [google_bigquery_table.instance_utilization_views](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_table) | resource |
| [google_bigquery_table.project_utilization_views](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_table) | resource |
| [google_cloud_scheduler_job.asset_export_job](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/cloud_scheduler_job) | resource |
| [google_cloud_scheduler_job.utilization_export_job](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/cloud_scheduler_job) | resource |
| [google_organization_iam_binding.organization](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/organization_iam_binding) | resource |
| [google_pubsub_subscription.bigquery_sub](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/pubsub_subscription) | resource |
| [google_pubsub_subscription.metrics_sub](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/pubsub_subscription) | resource |
| [google_pubsub_topic.topics](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/pubsub_topic) | resource |
| [local_file.foo](https://registry.terraform.io/providers/hashicorp/local/latest/docs/resources/file) | resource |
| [null_resource.export_asset_inventory_data](https://registry.terraform.io/providers/hashicorp/null/latest/docs/resources/resource) | resource |
| [google_project.project](https://registry.terraform.io/providers/hashicorp/google/latest/docs/data-sources/project) | data source |
| [template_file.bq_views](https://registry.terraform.io/providers/hashicorp/template/latest/docs/data-sources/file) | data source |
| [template_file.config_file](https://registry.terraform.io/providers/hashicorp/template/latest/docs/data-sources/file) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_activate_apis"></a> [activate\_apis](#input\_activate\_apis) | The list of apis to activate within the project | `list(string)` | `[]` | no |
| <a name="input_asset_export_scheduler_job_config"></a> [asset\_export\_scheduler\_job\_config](#input\_asset\_export\_scheduler\_job\_config) | Asset Export Cloud Scheduler Job Config | <pre>object({<br>    schedule         = string,<br>    attempt_deadline = string,<br>    http_method      = string<br>  })</pre> | <pre>{<br>  "attempt_deadline": "1800s",<br>  "http_method": "GET",<br>  "schedule": "0 */2 * * *"<br>}</pre> | no |
| <a name="input_bq_org_asset_inventory_dataset"></a> [bq\_org\_asset\_inventory\_dataset](#input\_bq\_org\_asset\_inventory\_dataset) | BiqQuery Asset Inventory Dataset Name | `string` | n/a | yes |
| <a name="input_bq_org_asset_inventory_tables_prefix"></a> [bq\_org\_asset\_inventory\_tables\_prefix](#input\_bq\_org\_asset\_inventory\_tables\_prefix) | BiqQuery Asset Inventory Table Prefix | `string` | `"org"` | no |
| <a name="input_bq_utlization_dataset"></a> [bq\_utlization\_dataset](#input\_bq\_utlization\_dataset) | BiqQuery Utilization Dataset Name | `string` | n/a | yes |
| <a name="input_cloud_run_config"></a> [cloud\_run\_config](#input\_cloud\_run\_config) | Cloud Run Configuration | <pre>object({<br>    service_name          = string,<br>    timeout_seconds       = number,<br>    container_concurrency = number,<br>    limits                = map(string),<br>    template_annotations  = map(string)<br>  })</pre> | <pre>{<br>  "container_concurrency": 10,<br>  "limits": {<br>    "cpu": "1000m",<br>    "memory": "1024M"<br>  },<br>  "service_name": "utilization-export",<br>  "template_annotations": {<br>    "autoscaling.knative.dev/maxScale": "200"<br>  },<br>  "timeout_seconds": 1800<br>}</pre> | no |
| <a name="input_cloudrun_image_version"></a> [cloudrun\_image\_version](#input\_cloudrun\_image\_version) | Cloud Run Image Version | `string` | n/a | yes |
| <a name="input_cloudrun_service_annotation"></a> [cloudrun\_service\_annotation](#input\_cloudrun\_service\_annotation) | Cloud Run Service Annotations | `map(string)` | <pre>{<br>  "run.googleapis.com/ingress": "all",<br>  "run.googleapis.com/operation-id": "445d22d7-bdf9-42b3-b379-e3856fa814ae"<br>}</pre> | no |
| <a name="input_config_tmpl_name"></a> [config\_tmpl\_name](#input\_config\_tmpl\_name) | Config Template File Name | `string` | `"config.yaml.tmpl"` | no |
| <a name="input_create_cloudrun_sa"></a> [create\_cloudrun\_sa](#input\_create\_cloudrun\_sa) | Set to true if you want to create service account for Cloud Run | `bool` | `true` | no |
| <a name="input_create_invoker_sa"></a> [create\_invoker\_sa](#input\_create\_invoker\_sa) | Set to true if you want to create invoker Service Account | `bool` | `false` | no |
| <a name="input_default_app_engine_location"></a> [default\_app\_engine\_location](#input\_default\_app\_engine\_location) | Default App Engine Location | `string` | `"us-central"` | no |
| <a name="input_enable_apis"></a> [enable\_apis](#input\_enable\_apis) | Set to true if you want to enable service APIs | `bool` | `true` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | Environment Name | `string` | n/a | yes |
| <a name="input_location"></a> [location](#input\_location) | Location to create BigQuery Dataset | `string` | `"US"` | no |
| <a name="input_mql_time_window"></a> [mql\_time\_window](#input\_mql\_time\_window) | MQL Time Window | `string` | `"1h"` | no |
| <a name="input_organization_id"></a> [organization\_id](#input\_organization\_id) | Organization ID | `string` | n/a | yes |
| <a name="input_project_id"></a> [project\_id](#input\_project\_id) | Project ID where all this will be steup . | `string` | n/a | yes |
| <a name="input_pubsub_bigquery_subscription_config"></a> [pubsub\_bigquery\_subscription\_config](#input\_pubsub\_bigquery\_subscription\_config) | Pub/Sub BigQuery Subscription Config | <pre>object({<br>    subcription_name           = string,<br>    topic_name                 = string,<br>    dead_letter_topic_name     = string,<br>    ack_deadline_seconds       = number,<br>    message_retention_duration = string,<br>    service_account_email      = string,<br>    max_delivery_attempts      = number,<br>    minimum_backoff            = string<br>  })</pre> | <pre>{<br>  "ack_deadline_seconds": 60,<br>  "dead_letter_topic_name": "dead-letter",<br>  "max_delivery_attempts": 5,<br>  "message_retention_duration": "1200s",<br>  "minimum_backoff": "60s",<br>  "service_account_email": "",<br>  "subcription_name": "bigquery-sub",<br>  "topic_name": "bigquery"<br>}</pre> | no |
| <a name="input_pubsub_metrics_subscription_config"></a> [pubsub\_metrics\_subscription\_config](#input\_pubsub\_metrics\_subscription\_config) | Pub/Sub Metrics Subscription Config | <pre>object({<br>    subcription_name           = string,<br>    topic_name                 = string,<br>    dead_letter_topic_name     = string,<br>    ack_deadline_seconds       = number,<br>    message_retention_duration = string,<br>    service_account_email      = string,<br>    max_delivery_attempts      = number,<br>    minimum_backoff            = string<br>  })</pre> | <pre>{<br>  "ack_deadline_seconds": 60,<br>  "dead_letter_topic_name": "dead-letter",<br>  "max_delivery_attempts": 5,<br>  "message_retention_duration": "1200s",<br>  "minimum_backoff": "60s",<br>  "service_account_email": "",<br>  "subcription_name": "metrics-sub",<br>  "topic_name": "metrics"<br>}</pre> | no |
| <a name="input_pubsub_topics"></a> [pubsub\_topics](#input\_pubsub\_topics) | List of Pub/Sub Topics | `list(string)` | <pre>[<br>  "metrics",<br>  "dead-letter",<br>  "bigquery"<br>]</pre> | no |
| <a name="input_region"></a> [region](#input\_region) | Region Name | `string` | n/a | yes |
| <a name="input_service_account"></a> [service\_account](#input\_service\_account) | Existing Service Account for Cloud Run. Provide only if you not create service account by setting create\_cloudrun\_sa to false | `string` | `""` | no |
| <a name="input_service_account_name"></a> [service\_account\_name](#input\_service\_account\_name) | Service Account Name for Cloud Run | `string` | `"utilization-export"` | no |
| <a name="input_utilization_scheduler_job_config"></a> [utilization\_scheduler\_job\_config](#input\_utilization\_scheduler\_job\_config) | Utilization Cloud Scheduler Job Config | <pre>object({<br>    schedule         = string,<br>    attempt_deadline = string,<br>    http_method      = string<br>  })</pre> | <pre>{<br>  "attempt_deadline": "1800s",<br>  "http_method": "GET",<br>  "schedule": "0 */2 * * *"<br>}</pre> | no |
| <a name="input_utilization_table_config"></a> [utilization\_table\_config](#input\_utilization\_table\_config) | Utilization Table Cofiguration | <pre>object({<br>    clustering = list(string),<br>    time_partitioning = object({<br>      expiration_ms            = string,<br>      field                    = string,<br>      type                     = string,<br>      require_partition_filter = bool,<br>    }),<br>    range_partitioning = object({<br>      field = string,<br>      range = object({<br>        start    = string,<br>        end      = string,<br>        interval = string,<br>      }),<br>    }),<br>    expiration_time = string,<br>    labels          = map(string),<br>  })</pre> | <pre>{<br>  "clustering": [],<br>  "expiration_time": null,<br>  "labels": {},<br>  "range_partitioning": null,<br>  "time_partitioning": {<br>    "expiration_ms": null,<br>    "field": null,<br>    "require_partition_filter": false,<br>    "type": "DAY"<br>  }<br>}</pre> | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_bigquery_asset_inventory_dataset"></a> [bigquery\_asset\_inventory\_dataset](#output\_bigquery\_asset\_inventory\_dataset) | BigQuery Org Asset Inventory Dataset |
| <a name="output_bigquery_subscription_id"></a> [bigquery\_subscription\_id](#output\_bigquery\_subscription\_id) | BigQuery Pub/Sub Subscription ID |
| <a name="output_bigquery_utlization_dataset"></a> [bigquery\_utlization\_dataset](#output\_bigquery\_utlization\_dataset) | BigQuery Utilization Dataset |
| <a name="output_bigquery_utlization_tables"></a> [bigquery\_utlization\_tables](#output\_bigquery\_utlization\_tables) | BigQuery Utilization Tables |
| <a name="output_bq_tables"></a> [bq\_tables](#output\_bq\_tables) | BQ Tables |
| <a name="output_cloudrun_revision"></a> [cloudrun\_revision](#output\_cloudrun\_revision) | Cloud Run Service Revision |
| <a name="output_cloudrun_service_name"></a> [cloudrun\_service\_name](#output\_cloudrun\_service\_name) | Cloud Run Service Name |
| <a name="output_cloudrun_service_status"></a> [cloudrun\_service\_status](#output\_cloudrun\_service\_status) | Cloud Run Service Status |
| <a name="output_cloudrun_service_url"></a> [cloudrun\_service\_url](#output\_cloudrun\_service\_url) | Cloud Run Service URL |
| <a name="output_config_file"></a> [config\_file](#output\_config\_file) | Config File Template Rendered Value |
| <a name="output_enabled_apis"></a> [enabled\_apis](#output\_enabled\_apis) | List of APIs Enabled |
| <a name="output_metrics_subscription_id"></a> [metrics\_subscription\_id](#output\_metrics\_subscription\_id) | Metrics Pub/Sub Subscription ID |
| <a name="output_pubsub_topics"></a> [pubsub\_topics](#output\_pubsub\_topics) | Pub/Sub Topics |
| <a name="output_service_account"></a> [service\_account](#output\_service\_account) | Cloud Run Service Account |
| <a name="output_tables_list"></a> [tables\_list](#output\_tables\_list) | List of BigQuery Tables |
| <a name="output_view_template_file"></a> [view\_template\_file](#output\_view\_template\_file) | BigQuery Views Template Rendered Value |
| <a name="output_views_list"></a> [views\_list](#output\_views\_list) | List of BigQuery Views |
