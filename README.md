# ElasticSearch

## Features

This module will deploy a brand new AWS ElasticSearch domain to a VPC. It can be used for creating the EFK stack or any other needed ElasticSearch services.

## Requirements

* [Pre Commit](https://github.com/pre-commit/pre-commit-hooks)
* [Terraform](https://www.terraform.io)
* [Terraform Docs](https://github.com/terraform-docs/terraform-docs/)

### Pre Commit

Please read the [Pre Commit](PRE_COMMIT.md) documentation for more information on how to install and use the pre-commit hooks.

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.14 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | ~> 3.0, < 4.0.0 |

## Resources

| Name | Type |
|------|------|
| [aws_cloudwatch_log_group.logs](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_log_group) | resource |
| [aws_cloudwatch_log_resource_policy.logs_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_log_resource_policy) | resource |
| [aws_elasticsearch_domain.es_domain](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/elasticsearch_domain) | resource |
| [aws_iam_service_linked_role.es](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_service_linked_role) | resource |
| [aws_security_group.es](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_caller_identity.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_domain"></a> [domain](#input\_domain) | Name of Elasticsearch domain to create | `string` | n/a | yes |
| <a name="input_elasticsearch_version"></a> [elasticsearch\_version](#input\_elasticsearch\_version) | Version of Elasticsearch to use | `string` | n/a | yes |
| <a name="input_instance_count"></a> [instance\_count](#input\_instance\_count) | Number of Elasticsearch nodes to create | `string` | n/a | yes |
| <a name="input_instance_type"></a> [instance\_type](#input\_instance\_type) | AWS instance type to use for Elasticsearch nodes. | `string` | n/a | yes |
| <a name="input_private_subnets"></a> [private\_subnets](#input\_private\_subnets) | Subnet IDs that can access Elasticsearch (once created). Typically the worker security group ID created by the EKS module. | `list(string)` | n/a | yes |
| <a name="input_private_subnets_cidrs"></a> [private\_subnets\_cidrs](#input\_private\_subnets\_cidrs) | The CIDR of IPs that should be able to access Elasticsearch. Typically the CIDR of worker nodes created by the EKS module. | `list(string)` | n/a | yes |
| <a name="input_region"></a> [region](#input\_region) | AWS region to create resources within | `string` | n/a | yes |
| <a name="input_volume_size"></a> [volume\_size](#input\_volume\_size) | Size of disk provisioned for Elasticsearch instances in GB. | `string` | n/a | yes |
| <a name="input_vpc_id"></a> [vpc\_id](#input\_vpc\_id) | VPC ID to create Elasticsearch domain within. | `string` | n/a | yes |
| <a name="input_create_iam_service_linked_role"></a> [create\_iam\_service\_linked\_role](#input\_create\_iam\_service\_linked\_role) | Create an AWS Service-Linked Role for use by Elasticsearch. The service linked role is used to provide the Elasticsearch cluster with the appropriate permissions to run. This should be 'true' for the first Elasticsearch cluster you create, and 'false' thereafter. (Only one service-linked role can be created per AWS account and it is shared by all ES domains.) More info at https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html | `string` | `true` | no |
| <a name="input_create_log_group"></a> [create\_log\_group](#input\_create\_log\_group) | Boolean that defines if the Log Group will be created or not | `bool` | `false` | no |
| <a name="input_dedicated_master_count"></a> [dedicated\_master\_count](#input\_dedicated\_master\_count) | Determines how many dedicated master should be created (dedicated\_master\_enabled should be ture) | `number` | `3` | no |
| <a name="input_dedicated_master_enabled"></a> [dedicated\_master\_enabled](#input\_dedicated\_master\_enabled) | Determines if a dedicated master insatance is needed | `bool` | `false` | no |
| <a name="input_dedicated_master_type"></a> [dedicated\_master\_type](#input\_dedicated\_master\_type) | Determines the type of dedicated master instances that should be created (dedicated\_master\_enabled should be ture) | `string` | `"c5.large.elasticsearch"` | no |
| <a name="input_ebs_type"></a> [ebs\_type](#input\_ebs\_type) | Ebs type of volume | `string` | `"gp2"` | no |
| <a name="input_encrypt_at_rest"></a> [encrypt\_at\_rest](#input\_encrypt\_at\_rest) | Whether or not to use encryption-at-rest for the newly created elasticsearch cluster. Needs to be disabled if using older instance types like t2 and m3 that do not support encryption. | `bool` | `true` | no |
| <a name="input_multiaz"></a> [multiaz](#input\_multiaz) | Determines if the elasticsearch should be deployed to two AZs. (Default false) | `bool` | `false` | no |
| <a name="input_node_to_node_encryption"></a> [node\_to\_node\_encryption](#input\_node\_to\_node\_encryption) | Whether or not to use node-node encryption for the newly created ES domain. Requires `elasticsearch_version` version >= 6 | `string` | `false` | no |
| <a name="input_tags"></a> [tags](#input\_tags) | A set of AWS tags to tag the resulting Elasticsearch cluster with. | `map(string)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_endpoint"></a> [endpoint](#output\_endpoint) | Domain-specific HTTPS endpoint used to submit index, search, and data upload requests. |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
