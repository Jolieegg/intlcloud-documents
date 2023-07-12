## Overview

You can log in to the [CLS console](https://console.cloud.tencent.com/cls) and ship data in CSV format to COS. This document describes how to create a CSV shipping task.

## Prerequisite

1. You have activated CLS, created a logset and a log topic, and successfully collected the log data.
2. You have activated COS and created a bucket in the target region for log topic shipping. For more information, see [Creating Bucket](https://intl.cloud.tencent.com/document/product/436/13309).
3. Sub-accounts and collaborators need to be authorized by the root account. For more information on granting permissions, see [CAM Access Management](https://intl.cloud.tencent.com/document/product/614/32854). For more information on copying authorization policies, see [Examples of Custom Access Policies](https://intl.cloud.tencent.com/document/product/614/45004).
4. You have authorized the CLS service role to access COS. If you perform operations in the console, the system will guide you through the authorization process. If you directly call APIs, manual authorization will be required. For more information, see [Viewing and Configuring Shipping Permissions](https://www.tencentcloud.com/document/product/614/46142).


## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Log Topic** on the left sidebar.
3. Click the desired log topic ID/name to go to the log topic management page.
4. Select the **Ship to COS** tab and click **Add Shipping Configuration**.
5. Set the following configuration items.

<b>The configuration items are as described below:</b>
<table>
   <tr>
      <th>Configuration Item</th>
      <th>Description</th>
      <th>Limit</th>
      <th>Required</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Shipping Task Name</td>
      <td>Configures the name of a shipping task</td>
      <td nowrap="nowrap">The name can contain letters, numbers, underscores (_), and hyphens (-)</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">COS Bucket</td>
      <td>Target bucket for shipping. The target bucket must be in the same region as the current log topic.</td>
      <td>A value selected from the drop-down list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>COS Path</td>
      <td>COS bucket path, which is in the format of `/year/month/day/hour/` by default, such as `/2022/7/31/14/`. This format is used in COS for storing shipped log files. Here, the <a href="http://man7.org/linux/man-pages/man3/strptime.3.html">strftime</a> syntax is supported. For example, if a log was shipped at 14:00 on July 31, 2022, the generated `/%Y/%m/%d/` path is `/2022/7/31/`, and the `/%Y%M%d/%H/` path is `/2022/07/31/14/`.</td>
      <td>Cannot start with <code>/</code></td>
      <td>No</td>
   </tr>
   <tr>
      <td>Filename</td>
	  <td>Option 1 (recommended): Use the shipping time as the name. For example, `202208251645_000_132612782.gz` indicates the shipping time_log topic partition_offset. This type of files can be loaded in Hive.</br>
Option 2: Use a random number as the name. This is the legacy practice of naming files and cannot be recognized by Hive as it cannot recognize filenames starting with "_". You can add a custom prefix to the COS path, such as `/%Y%M%d/%H/Yourname`.</td>
      <td>/</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Compression Format</td>
			<td>To reduce read traffic fees, log files are compressed before being shipped to COS. Snappy, lzop, and GZIP are supported.</td>
      <td>GZIP, Snappy, and lzop</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">File Size</td>
      <td>It indicates the size of the raw log file to be shipped and is used together with the shipping interval parameter. When either condition is met, compression will be performed accordingly. For example, if the size is set to 256 MB and the interval is set to 15 minutes, when the file reaches 256 MB within five minutes, the size condition will be met first to trigger shipping.</td>
      <td nowrap="nowrap">The value must be a number ranging from 5 to 256 in MB.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Shipping Interval</td>
      <td>It indicates the interval for shipping and is used together with the file size parameter. When either condition is met, compression will be performed accordingly. For example, if the size is set to 256 MB and the interval is set to 15 minutes, when the file reaches only 200 MB in 15 minutes, the shipping interval condition will be met first to trigger shipping.</td>
      <td>Value range: 300-900s</td>
      <td>Yes</td>
   </tr>
</table>
6. Click **Next** to enter the **Advanced Configuration** page. Set **Shipping Format** to **CSV** and set the configuration items.

<b>The configuration items are as described below:</b>
<table>
   <tr>
      <th>Configuration Item</th>
      <th>Description</th>
      <th>Limit</th>
      <th>Required</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Key</td>
      <td>Specifies the key name of the written CSV file. The value must be the key name or reserved parameter after logs are structured. Otherwise, the value is invalid.</td>
      <td nowrap="nowrap">The name can contain letters, numbers, underscores (_), and hyphens (-)</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Separator</td>
      <td>Separators between the fields in the CSV file</td>
      <td>A value selected from the drop-down list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Escape Character</td>
      <td>If the normal fields contain the selected separator characters, the separators will be enclosed by escape characters to prevent incorrect identification during data reading.</td>
      <td>A value selected from the drop-down list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Invalid Field Filling</td>
      <td>If the configured key field does not exist, an invalid field is filled in.</td>
      <td>A value selected from the drop-down list</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Key in First Line</td>
      <td>Adds field name description to the first line of the CSV file. That is, the key value is written into the first line of the CSV file. This is disabled by default.</td>
      <td>Enabled/Disabled</td>
      <td>Yes</td>
   </tr>
</table>
