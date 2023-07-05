This document describes how to enable sub-accounts to view and use the TCR Enterprise related resources through the CAM policy, including specific operation steps and common policy configuration examples.

>! If you need the permissions of other Tencent Cloud services when using some features in TCR console such as VPC, CloudAudit, Tag, please see the corresponding CAM Guide in [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).



## Directions
This document takes the example of "granting the sub-account the read-only permission of an image repository" to introduce how to create a policy.

- **Instance ID**: tcr-xxxxxxxx
- **Namespace**: team-01
- **Image repository**: repo-demo

<dx-tabs>
::: Creating by policy generator (recommended)
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. In the left sidebar, click **Policies** to go to the policy management page.
3. Click **Create custom policy** in the upper-left corner.
4. In the pop-up window, click **Create by policy generator** to go to the **Edit policy** page.
5. Select the service in the Visual Policy Generator, enter the following information, and edit an authorization statement. 
 - **Effect**: Select **Allow** or **Deny**. Here, we select **Allow**.
 - **Service**: Select the service you want to authorize. Here, we select **Tencent Container Registry (tcr)**.
 - **Action**: Select the operations you want to authorize. Here, we select **Read**.
 - **Resource**: Select all resources or specific resources you want to authorize. Here, we select **Specific resources**, and add the following six-segment resource to restrict the access.
	 - **repository**: Select the region where the repository resides, and enter the resource path of the repository, for example, `tcr-xxxxxxxx/team-01/repo-demo/*`. You can get the resource path in [Image Repository](https://console.cloud.tencent.com/tcr/repository).
	 - **repo**: It is left empty.
	 - **instance**: Select the region where the repository resides, and enter the ID of the instance to which the repository belongs, for example, `tcr-xxxxxxxx`. You can get the instance ID in the [Instance List](https://console.cloud.tencent.com/tcr/instance?rid=1).
 - **Condition**: It is left empty.
6. Click **Next** to go to the **Associate users/user groups** page.
7. On the **Associate users/user groups** page, add the policy name and description, and you can associate users or user groups for quick authorization at the same time.
8. Click **Complete** to complete the custom policy creation.


:::
::: Creating by policy syntax
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. In the left sidebar, click **Policies** to go to the policy management page.
3. Click **Create custom policy** in the upper-left corner.
4. In the selection window that pops up, click **Create by policy syntax** to go to the **Select policy template** page.
5. In **Select a template type** section, select **Blank template**.
6. Click **Next** to go to the **Edit policy** page.
7. In the **Edit policy** page, enter the policy name and description, and add the following policy content.
```
	{
		"version": "2.0",
		"statement": [{
				"action": [
					"tcr:DescribeRepositories",
					"tcr:PullRepository",
					"tcr:DescribeNamespaces"
				],
				"resource": [
					"qcs::tcr:::repository/tcr-xxxxxxxx/team-01/repo-demo/*"
				],
				"effect": "allow"
			},
			{
				"action": [
					"tcr:DescribeInstance*"				
				],
				"resource": [
					"qcs::tcr:::instance/tcr-xxxxxxxx"
				],
				"effect": "allow"
			}
		]
	}
```
8. Click **Complete** to complete the custom policy creation.


:::
</dx-tabs>


















## Common Policy Configuration

If you need to customize the policy JSON, please see [CAM APIs for TCR Enterprise](https://intl.cloud.tencent.com/document/product/1051/39860) and [Syntax Logic](https://intl.cloud.tencent.com/document/product/598/10603).

### Preset policy configuration
- **QcloudTCRFullAccess**: Full read/write permission of TCR.
After the policy is bound to a sub-account, the sub-account has all operation permissions for all TCR resources, including TCR Enterprise and TCR Individual.
```json
	{
		"version": "2.0",
		"statement": [{
			"action": [
				"tcr:*"
			],
			"resource": "*",
			"effect": "allow"
		}]
	}
```
- **QcloudTCRReadOnlyAccess**: Read-only permission of TCR.
After the policy is bound to a sub-account, the sub-account has the read-only permission for all TCR resources, including the TCR Enterprise and TCR Individual.
```json
	{
		"version": "2.0",
		"statement": [{
			"action": [
				"tcr:Describe*",
				"tcr:PullRepository*"
			],
			"resource": "*",
			"effect": "allow"
		}]
	}
```

### Policy configuration in typical scenarios
>!The following scenario policies are only used for TCR Enterprise use cases. For the policies used for TCR Individual, please see [Example of Authorization Solution of TCR Individual](https://intl.cloud.tencent.com/document/product/1051/37250).
>
- Grant a sub-account all read/write operation permissions for all resources in TCR Enterprise.
```json
	{
		"version": "2.0",
		"statement": [{
			"action": [
				"tcr:*"
			],
			"resource": [
				"qcs::tcr:::instance/*",
				"qcs::tcr:::repository/*"
			],
			"effect": "allow"
		}]
	}
```
- Grant a sub-account the read-only permission for all resources in TCR Enterprise.
```json
	{
		"version": "2.0",
		"statement": [{
			"action": [
				"tcr:Describe*",
				"tcr:PullRepository*"
			],
			"resource": [
				"qcs::tcr:::instance/*",
				"qcs::tcr:::repository/*"
			],
			"effect": "allow"
		}]
	}
```
- Grant a sub-account permissions to manage the specified instance, for example, dev-guangzhou, whose instance ID is tcr-xxxxxxxx.
```json
	{
		"version": "2.0",
		"statement": [{
			"action": [
				"tcr:*"
			],
			"resource": [
				"qcs::tcr:::instance/tcr-xxxxxxxx",
				"qcs::tcr:::repository/tcr-xxxxxxxx/*"
			],
			"effect": "allow"
		}]
	}
```
- Grant a sub-account permissions to manage the specified namespace in the specified instance, for example, team-01 under the instance tcr-xxxxxxxx.
```json
	{
		"version": "2.0",
		"statement": [{
				"action": [
					"tcr:*"
				],
				"resource": [
					"qcs::tcr:::repository/tcr-xxxxxxxx/team-01",
					"qcs::tcr:::repository/tcr-xxxxxxxx/team-01/*"
				],
				"effect": "allow"
			},
			{
				"action": [
					"tcr:DescribeInstance*"
				],
				"resource": [
					"qcs::tcr:::instance/tcr-xxxxxxxx"
				],
				"effect": "allow"
			}
		]
	}
```
- Grant a sub-account the read-only permission of an image repository, which means that the sub-account can only pull the images in the image repository instead of deleting a repository, modifying repository attributes, or pushing images, for example, repo-demo in the namespace team-01 under the instance tcr-xxxxxxxx.
```json
	{
		"version": "2.0",
		"statement": [{
				"action": [
					"tcr:Describe*",
					"tcr:PullRepository"
				],
				"resource": [
					"qcs::tcr:::instance/tcr-xxxxxxxx",
					"qcs::tcr:::repository/tcr-xxxxxxxx/team-01",
					"qcs::tcr:::repository/tcr-xxxxxxxx/team-01/repo-demo",
					"qcs::tcr:::repository/tcr-xxxxxxxx/team-01/repo-demo/*"
				],
				"effect": "allow"
			}
		]
	}
```
