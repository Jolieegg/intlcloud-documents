## 现象描述

使用内容分发网络（Content Delivery Network，CDN）域名访问对象存储（Cloud Object Storage，COS）时，返回 HTTP ERROR 403 错误码。


## 可能原因

CDN 加速域名为关闭状态。

## 处理步骤

1. 登录 [对象存储控制台](https://console.cloud.tencent.com/cos5)。
2. 在左侧导航栏中，选择**存储桶列表**，进入存储桶管理页面。
3. 找到需要操作的存储桶，单击该存储桶名称，进入存储桶配置页面。
4. 在左侧导航栏中，选择**域名与传输管理 > 默认 CDN 加速域名**，进入默认 CDN 加速域名页面。
5. 在“默认 CDN 加速域名”栏中，检查当前状态是否为关闭状态。
 - 是，请 [开启默认 CDN 加速域名](https://intl.cloud.tencent.com/document/product/436/31505)。
 - 否，请执行下一步。
6. 在“自定义 CDN 加速域名”栏中，检查状态是否为已上线。
 - 是，请 [联系我们](https://intl.cloud.tencent.com/support)。
 - 否，请 [开启自定义 CDN 加速域名](https://intl.cloud.tencent.com/document/product/436/31506)。

