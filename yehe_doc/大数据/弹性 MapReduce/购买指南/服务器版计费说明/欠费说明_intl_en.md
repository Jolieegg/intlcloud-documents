## Pay-As-You-Go
### Overdue payment alerts

| Type | Description |
| ------------ | ------------------------------------------------------------ |
| **Overdue payment reminder** | Pay-as-you-go clusters are billed on the hour. When your account balance becomes negative, your Tencent Cloud account creator, global resource collaborators, and financial collaborators will be notified by email and SMS. |
| **Balance alert** | This feature is disabled by default. To enable it, see "Balance Notifications". |

### Overdue policy
When your account balance falls below zero, a pay-as-you-go cluster can be used for 2 more hours, and the usage will still be deducted from your account. After 2 hours, the cluster will be moved to the recycle bin and become unavailable, and will no longer incur pay-as-you-go costs.

<table>
<tr>
<th>Time After Service Suspension</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="2">≤ 15 days</td>
<td>If your account is topped up to a positive balance, the charging will continue, and the cluster will be automatically recovered.</td>
</tr>
<tr>
<td>If your account balance remains negative, the cluster cannot be recovered.</td>
</tr>
<tr>
<td >> 15 days</td>
<td>If your account is not topped up to a positive balance, your pay-as-you-go cluster resources will be repossessed and released. All data will be cleared and cannot be recovered. When your cluster resources are repossessed, your Tencent Cloud account creator and all collaborators will be notified by email and SMS.</td>
</tr>
</table>

>!
- If a pay-as-you-go cluster is no longer needed, terminate it as soon as possible to avoid incurring further costs.
- After a cluster is terminated, the data in it will be cleared and cannot be recovered.
- Because your resource usage changes constantly, the balance alerts may not be precisely accurate.
- You will continue to be charged for associated cloud products such as EIP and CBS during cluster isolation due to overdue payments until your account balance becomes negative.

## Overdue Payments of Associated Cloud Products
| Product              | Description                                           |
| --------------------- | ------------------------------------------------------------ |
| EIP | Elastic IP Payment Overdue|
| TencentDB for MySQL (CDB) | [Payment Overdue](https://intl.cloud.tencent.com/document/product/236/5159) |
| CBS             | [Payment Overdue](https://intl.cloud.tencent.com/document/product/362/31625) |
| COS          | [Payment Overdue](https://intl.cloud.tencent.com/document/product/436/10044) |
| CHDFS      | [Payment Overdue](https://intl.cloud.tencent.com/document/product/1106/41955) |
| VPC          |  [Overdue Payment Alert](https://intl.cloud.tencent.com/document/product/1003/30054) <br> [Payment Overdue](https://intl.cloud.tencent.com/document/product/553/35176) |

