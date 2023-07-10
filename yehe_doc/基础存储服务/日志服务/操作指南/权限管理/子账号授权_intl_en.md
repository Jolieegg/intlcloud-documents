## Overview

[CAM](https://www.tencentcloud.com/document/product/598) is a web-based Tencent Cloud service that helps you securely manage and control access to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (user groups), and control who can access and use your Tencent Cloud resources through identity and policy management. For more information on CAM policies and how to use them, see [Concepts](https://intl.cloud.tencent.com/document/product/598/10600).

A root account can grant a sub-account or collaborator access to specified CLS resources.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0263a15f4d92eba1cfca76421416b0dc.png" width="80%">

## Preset access policies

CLS offers two preset access policies to meet your basic access management demand.
- QcloudCLSFullAccess: access to all CLS resources and actions, including creating log topics, modifying index configuration, deleting log topics, searching for logs, uploading logs, etc.
- QcloudCLSReadOnlyAccess: only read access to CLS data; no CRUD access

For how to use the policies, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

## Custom access policies

You can use a custom access policy to grant access at a finer granularity, for example, to allow a specific user to view the data of a specific log topic.

A custom access policy consists of two parts:
- Action: The action a user is allowed to perform, such as searching for logs, modifying index configuration, uploading logs, and creating alarm policies.
- Resource: The resources a user is allowed to operate on, such as a specific log topic, dashboard, and data processing task.

For more information on authorizable resource types and APIs of CLS, see [Authorizable Resource Types](https://intl.cloud.tencent.com/document/product/614/45877). For more information on configuration methods, see [Creating Custom Policy](https://intl.cloud.tencent.com/document/product/598/35596).

Configuring custom access policies can be a demanding process. The examples we offer in [Access Policy Templates](https://intl.cloud.tencent.com/document/product/614/45004) should meet most access management needs. You can also modify the examples based on your requirements. Detailed directions are as follows:
1. Log in to the console with the root account (or an account with CAM access). On the [Policies](https://console.cloud.tencent.com/cam/policy) page, click **Create Custom Policy**.

2. In the pop-up window, click **Create by Policy Syntax**.
3. On the **Select Policy Template** page, select **Blank Template** and click **Next**.
4. On the **Edit Policy** page, enter a policy name and policy content. For the latter, you can copy the content from [Access Policy Templates](https://intl.cloud.tencent.com/document/product/614/45004). For example, to grant the sub-account permission to use LogListener, copy the policy as shown below:

5. Click **Complete** to save the policy. Then, you can associate it with a user/user group to grant the user/user group the corresponding operation permissions as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
