<!-- BEGIN_TF_DOCS -->
## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |
| <a name="provider_cloudinit"></a> [cloudinit](#provider\_cloudinit) | n/a |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [aws_autoscaling_group.ecs_nodes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/autoscaling_group) | resource |
| [aws_ecs_capacity_provider.asg](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ecs_capacity_provider) | resource |
| [aws_ecs_cluster.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ecs_cluster) | resource |
| [aws_ecs_cluster_capacity_providers.example](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ecs_cluster_capacity_providers) | resource |
| [aws_iam_instance_profile.ecs_node](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_instance_profile) | resource |
| [aws_iam_role.ec2_instance_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role.ecs_service_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role.ecs_task_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role_policy.allow_create_log_groups](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy) | resource |
| [aws_iam_role_policy_attachment.default_task_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.ecs_instance_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.service_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.ssm_core_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_launch_template.node](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/launch_template) | resource |
| [aws_security_group.ecs_nodes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_security_group_rule.egress](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.ingress](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_iam_policy_document.allow_create_log_groups](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_iam_policy_document.ec2_instance_assume_role_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_iam_policy_document.ecs_service_role_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_iam_policy_document.ecs_task_role_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_ssm_parameter.ecs_ami](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/ssm_parameter) | data source |
| [aws_ssm_parameter.ecs_ami_arm64](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/ssm_parameter) | data source |
| [aws_subnet.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/subnet) | data source |
| [cloudinit_config.config](https://registry.terraform.io/providers/hashicorp/cloudinit/latest/docs/data-sources/config) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_cluster_name"></a> [cluster\_name](#input\_cluster\_name) | Cluster name. | `any` | n/a | yes |
| <a name="input_subnets_ids"></a> [subnets\_ids](#input\_subnets\_ids) | IDs of subnets. Use subnets from various availability zones to make the cluster more reliable. | `list(string)` | n/a | yes |
| <a name="input_arm64"></a> [arm64](#input\_arm64) | ECS node architecture. Default is `amd64`. You can change it to `arm64` by activating this flag. If you do, then you should use corresponding instance types. | `bool` | `false` | no |
| <a name="input_asg_max_size"></a> [asg\_max\_size](#input\_asg\_max\_size) | The maximum size the auto scaling group (measured in EC2 instances). | `number` | `100` | no |
| <a name="input_asg_min_size"></a> [asg\_min\_size](#input\_asg\_min\_size) | The minimum size the auto scaling group (measured in EC2 instances). | `number` | `0` | no |
| <a name="input_ebs_disks"></a> [ebs\_disks](#input\_ebs\_disks) | A list of additional EBS disks. | `map(string)` | `{}` | no |
| <a name="input_health_check_grace_period"></a> [health\_check\_grace\_period](#input\_health\_check\_grace\_period) | Time period in seconds that delays the first health check until your instances finish initializing. | `number` | `null` | no |
| <a name="input_instance_requirements"></a> [instance\_requirements](#input\_instance\_requirements) | ECS node instance requirements. An object specifying memory\_mib, vcpu\_count min and max. Pass null in for min or max for an empty value. Cannot be provided along with instance\_types. | <pre>list(object({<br>    memory_mib = list(object({<br>      min = number<br>      max = number<br>    }))<br>    vcpu_count = list(object({<br>      min = number<br>      max = number<br>    }))<br>  }))</pre> | <pre>[<br>  {<br>    "memory_mib": [<br>      {<br>        "max": 512000,<br>        "min": 512000<br>      }<br>    ],<br>    "vcpu_count": [<br>      {<br>        "max": 1,<br>        "min": 1<br>      }<br>    ]<br>  }<br>]</pre> | no |
| <a name="input_instance_types"></a> [instance\_types](#input\_instance\_types) | ECS node instance types. Maps of pairs like `type = weight`. Where weight gives the instance type a proportional weight to other instance types. Cannot be provided along with instance\_requirements. | `map(any)` | `{}` | no |
| <a name="input_lifecycle_hooks"></a> [lifecycle\_hooks](#input\_lifecycle\_hooks) | A list of lifecycle hook actions. See details at https://docs.aws.amazon.com/autoscaling/ec2/userguide/lifecycle-hooks.html. | <pre>list(object({<br>    name                    = string<br>    lifecycle_transition    = string<br>    default_result          = string<br>    heartbeat_timeout       = number<br>    role_arn                = string<br>    notification_target_arn = string<br>    notification_metadata   = string<br>  }))</pre> | `[]` | no |
| <a name="input_on_demand_base_capacity"></a> [on\_demand\_base\_capacity](#input\_on\_demand\_base\_capacity) | The minimum number of on-demand EC2 instances. | `number` | `0` | no |
| <a name="input_protect_from_scale_in"></a> [protect\_from\_scale\_in](#input\_protect\_from\_scale\_in) | The autoscaling group will not select instances with this setting for termination during scale in events. | `bool` | `true` | no |
| <a name="input_security_group_ids"></a> [security\_group\_ids](#input\_security\_group\_ids) | Additional security group IDs. Default security group would be merged with the provided list. | `list` | `[]` | no |
| <a name="input_spot"></a> [spot](#input\_spot) | Choose should we use spot instances or on-demand to populate ECS cluster. | `bool` | `false` | no |
| <a name="input_target_capacity"></a> [target\_capacity](#input\_target\_capacity) | The target utilization for the cluster. A number between 1 and 100. | `string` | `"100"` | no |
| <a name="input_trusted_cidr_blocks"></a> [trusted\_cidr\_blocks](#input\_trusted\_cidr\_blocks) | List of trusted subnets CIDRs with hosts that should connect to the cluster. E.g., subnets with ALB and bastion hosts. | `list(string)` | <pre>[<br>  ""<br>]</pre> | no |
| <a name="input_user_data"></a> [user\_data](#input\_user\_data) | A shell script will be executed at once at EC2 instance start. | `string` | `""` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_arn"></a> [arn](#output\_arn) | Cluster ARN. |
| <a name="output_capacity_provider_name"></a> [capacity\_provider\_name](#output\_capacity\_provider\_name) | capacity provider name (the same name for ASG). |
| <a name="output_ecs_default_task_role_arn"></a> [ecs\_default\_task\_role\_arn](#output\_ecs\_default\_task\_role\_arn) | ECS default task role ARN. |
| <a name="output_ecs_default_task_role_name"></a> [ecs\_default\_task\_role\_name](#output\_ecs\_default\_task\_role\_name) | ECS default task role name. |
| <a name="output_ecs_service_role_arn"></a> [ecs\_service\_role\_arn](#output\_ecs\_service\_role\_arn) | ECS service role ARN. |
| <a name="output_ecs_service_role_name"></a> [ecs\_service\_role\_name](#output\_ecs\_service\_role\_name) | ECS service role name. |
| <a name="output_iam_instance_profile_arn"></a> [iam\_instance\_profile\_arn](#output\_iam\_instance\_profile\_arn) | IAM instance profile ARN. |
| <a name="output_iam_instance_profile_name"></a> [iam\_instance\_profile\_name](#output\_iam\_instance\_profile\_name) | IAM instance profile name. |
| <a name="output_iam_instance_role_name"></a> [iam\_instance\_role\_name](#output\_iam\_instance\_role\_name) | IAM instance role name. |
| <a name="output_id"></a> [id](#output\_id) | Cluster ID. |
| <a name="output_name"></a> [name](#output\_name) | Cluster name. |
| <a name="output_security_group_id"></a> [security\_group\_id](#output\_security\_group\_id) | The ID of the ECS nodes security group. |
| <a name="output_security_group_name"></a> [security\_group\_name](#output\_security\_group\_name) | The name of the ECS nodes security group. |
<!-- END_TF_DOCS -->
