<span id="FeaturesOverview"></span>
## Features
Tencent Cloud CBS [snapshots](https://intl.cloud.tencent.com/document/product/362/31638) have the scheduled snapshot feature, which makes it easier for developers to flexibly set backup job policies.
The following table describes the scheduled snapshot policies recommended for different businesses.

<table>
	<tr>
		<th>Scenario</th>
		<th>Snapshot Policy</th>
		<th>Snapshot Retention Period</th>
	</tr>
	<tr>
		<td>Core product/service</td>
		<td>Use scheduled snapshots, with the policy set to once per day.</td>
		<td>7 to 30 days</td>
	</tr>
	<tr>
		<td>Non-core and non-data product/service</td>
		<td>Use scheduled snapshots, with the policy set to once per week.</td>
		<td>7 days</td>
	</tr>
	<tr>
		<td>Archive</td>
		<td>Scheduled snapshot is not required. You can create snapshots manually whenever needed.</td>
		<td>One month to several months</td>
	</tr>
	<tr>
		<td>Test</td>
		<td>Scheduled snapshot is not required. You can create snapshots manually whenever needed.</td>
		<td>Deleted after being used</td>
	</tr>
</table>


## Policy Description
The following table describes the content and features of scheduled snapshot policies, which help you better use snapshots in your businesses.
<table>
     <tr>
         <th>Item</th>  
         <th>Description</th>  
     </tr>
	 <tr>
         <td>Object</td>
         <td>All cloud disks, including system disks and data disks.</td>
     </tr> 
	 <tr>
         <td>Policy</td>
         <td>The point in time for scheduled snapshot creation can be accurate to every hour or every day. A scheduled snapshot policy is valid permanently after being set.</br>If you modify a scheduled snapshot policy, it takes effect immediately.</td>
     </tr>
	 <tr>
         <td nowrap="nowrap">Scheduled termination<b>(Important)</b></td>
         <td>Scheduled snapshots can be terminated periodically. After you set a snapshot lifecycle (1–30 days), scheduled snapshots are automatically deleted upon expiration, which reduces the backup costs.</br>If you do not set a scheduled termination policy, scheduled snapshots will be stored permanently.</td>
     </tr>
	 <tr>
         <td>Batch</td>
         <td>You can apply the same scheduled snapshot policy to multiple cloud disks.</td>
     </tr>
	 <tr>
         <td>Naming rules</td>
         <td>Scheduled snapshots are named in the format of snap_yyyyMMdd_HH. yyyyMMdd is the creation date, and HH is the creation hour. </br>You can manually modify snapshot names.</br>For example, snap_20180418_11 indicates a snapshot that was automatically created on 11:00 April 18, 2018.</td>
     </tr>
	 <tr>
         <td nowrap="nowrap">Lifecycle<b>(Important)</b></td>
         <td>Snapshot lifecycles vary depending on the snapshot creation method:<li>Manually created snapshots are <b>permanently stored</b> by default as long as the account balance is sufficient.</li><li>Scheduled snapshots can be <b>terminated periodically</b> or permanently stored.</li></td>
     </tr>
	 <tr>
         <td>Snapshot conflict</td>
         <td>Scheduled snapshots do not conflict with custom snapshots in use. However, they may conflict with each other on the creation time.</br><li>When a snapshot is automatically created for a disk, you can create a custom snapshot only after automatic snapshot creation is complete, and vice versa.</li><li>If there is a large amount of data on the disk and the time for automatically creating a snapshot exceeds the interval between two time points for automatic snapshot creation, a snapshot is not automatically created in the next time point. For example, if you set 9:00, 10:00, and 11:00 as the time points for automatic snapshot creation and it takes 70 minutes to create the snapshot at 9:00, a snapshot is not automatically created at 10:00 and is only created at 11:00.</li></td>
     </tr>
	 <tr>
         <td>Snapshot quota</td>
         <td>Each disk has a certain snapshot quota. If the number of snapshots on a disk has reached the quota limit, the scheduled snapshot task will be suspended or blocked.</br>The snapshot quota is used to prevent continuous increase in the storage costs if developers forget a scheduled snapshot policy.</td>
     </tr>
	 <tr>
         <td>ASP</td>
         <td>Indicates the scheduled snapshot policy, that is, Auto Snapshot Policy.</td>
     </tr>
	 <tr>
         <td>ASP quota</td>
         <td>A single Tencent Cloud account can set a maximum of 30 ASPs in each region. An ASP can be associated with a maximum of 200 cloud disks.</td>
     </tr>
	 <tr>
         <td>Retention period</td>
         <td><li>The console displays the repossession countdown for scheduled snapshots. You can manually change the retention period of scheduled snapshots to permanent.</li><li>Manually created snapshots are permanently stored.</td>
     </tr>
	 <tr>
         <td>ASP pause</td>
         <td><li>An ASP can be manually <b>paused</b>. After it is paused, snapshots are no longer automatically created. However, lifecycles of previously created snapshots are not affected by this function. They will be periodically terminated or permanently stored based on configured rules.</td>
     </tr>
	 <tr>
         <td>Operations logs</td>
         <td>Show the creation process of all scheduled snapshots, same as that of manually created snapshots.</td>
     </tr>
</table>


## Directions
### Creating a scheduled snapshot policy
>? A single Tencent Cloud account can set a maximum of 30 scheduled snapshot policies in each region.

1. Log in to the [Scheduled Snapshot Policy](https://console.cloud.tencent.com/cvm/snapshot/asp) page.
<span id="step2"></span>
2. Select a region.
3. Click **Create**, as shown in the following figure:

<span id="step4"></span>
4. On the **Create a new snapshot policy** page, set the following parameters and click **OK**, as shown in the following figure:
 <table>
     <tr>
         <th width="14%">Parameter</th>  
         <th>Description</th>  
     </tr>
	 <tr>
         <td>Name</td>
         <td>Required.</br>The name of a scheduled snapshot policy. It can contain up to 60 characters.</td>
     </tr> 
	 <tr>
         <td>Region</td>
         <td>Required.</br>This parameter cannot be changed on the current page. For more information on how to set this parameter, see <a href="#step2">Step 2</a>.</td>
     </tr>
	 <tr>
         <td>Backup Date</td>
         <td>Required.</br>The date for automatically creating snapshots. Value range: Sunday to Saturday.</td>
     </tr>
	 <tr>
         <td>Backup Time</td>
         <td>Required.</br>The time to automatically create snapshots. Value range: 00:00 - 23:00. Due to server performance issues, the actual scheduled snapshot creation time may be slightly different from time set here. In this case, data in a snapshot is based on the actual creation time.</td>
     </tr>
	 <tr>
         <td>Retention Period</td>
         <td>Required.<ul><li>Retained for a fixed number of days. The value range is 1 to 30 days. The default value is 30 days.</li><li>Permanent</li></ul></td>
     </tr>
</table>




### Associating with cloud disks
>? A scheduled snapshot policy can be associated with a maximum of 200 cloud disks.

1. Log in to the [Scheduled Snapshot Policy](https://console.cloud.tencent.com/cvm/snapshot/asp) page.
2. Select a region.
3. Find the target policy and click **Associate Cloud Disks**.
4. On the **Associate Cloud Disks** page, select cloud disks to associate with.
5. Click **OK**.

### Enabling or disabling a scheduled snapshot policy
1. Log in to the [Scheduled Snapshot Policy](https://console.cloud.tencent.com/cvm/snapshot/asp) page.
2. Select a region.
3. Find the target policy and click the button in the **Scheduled Snapshot** column to enable or disable the scheduled snapshot policy.

### Modifying a scheduled snapshot policy
1. Log in to the [Scheduled Snapshot Policy](https://console.cloud.tencent.com/cvm/snapshot/asp) page.
2. Select a region.
3. Find the target policy and click **Change Policy** in the **Operation** column.
4. In the **Modify snapshot policy** dialog box, modify related parameters and click **OK**. For more information about parameter descriptions, see [Step 4](#step4)).

### Deleting a scheduled snapshot policy

1. Log in to the [Scheduled Snapshot Policy](https://console.cloud.tencent.com/cvm/snapshot/asp) page.
2. Select a region.
3. Select either of the following methods to delete scheduled snapshot policies.
 a. To delete a single scheduled snapshot policy, find the target policy and choose **More** -> **Delete**.
 b. To delete multiple scheduled snapshot policies, select the scheduled snapshot policies to delete and click **Delete** above the scheduled snapshot list.

### Setting permanent storage for scheduled snapshots
>? If **Retention Period** is set to **Permanent** for a scheduled snapshot policy, you do not need to perform the following operations for snapshots automatically created using this policy.

1. Log in to the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page.
2. Select a region.
3. Click the ID of the target snapshot.
4. On the details page, click **Permanent** to permanently store the snapshot.
5. Return to the snapshot list. **Retention Period** of the snapshot is changed to **Permanent**.
