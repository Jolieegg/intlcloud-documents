

## Overview
The following describes how to configure fully managed and semi-managed migration tasks to migrate data from Alibaba Cloud OSS to Tencent Cloud COS.


## Preparations

#### Alibaba Cloud OSS
Create an RAM account and grant required permissions:
1.	Log in to the RAM console.
2.	Select **People Management** > **Users** > **Create User**.
3.	Select console password login and programming access, and then enter the user account information.
4.	Save the generated account, password, `AccessKeyID`, and `AccessKeySecret`.
5.	Select the user login name and click **Add Permissions** to grant the sub-account read and write permissions (AliyunOSSFullAccess).

#### Tencent Cloud COS
1. Create a bucket to store the migrated data as instructed in [Creating Bucket](https://www.tencentcloud.com/document/product/436/13309).
2. Create a sub-user for migration and grant the required permissions:
	1.	Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
	2.	Click **User** > **User List** on the left sidebar to enter the user list page.
	3.	Create a sub-user and select **Programming access** and **Tencent Cloud console access**.
	4.	Search for and select the `QcloudCOSAccessForMSPRole` and `QcloudCOSFullAccess` policies.
	5.	Complete creating the sub-user and save the sub-username, login password, `SecretId`, and `SecretKey`.


>?You can use Migration Service Platform (MSP) with your root account. However, for security reasons, we recommend you create a sub-account, use the sub-account's API key for migration, and delete the sub-user after migration.

## Directions

#### Logging in to MSP

1. Log in to the [MSP console](https://console.cloud.tencent.com/msp).
2. Click **Object Storage Migration** on the left sidebar.


#### Creating a migration task
1. On the **Object Storage Migration** page, click **Create a Task** to enter the object storage migration task configuration page and set migration parameters.

2. Set the migration task name.
    ![](https://qcloudimg.tencent-cloud.cn/raw/896762f3db5eede46e3437f054436854.png)
    **Task Name**: It can contain 1–60 letters, digits, underscores, and hyphens. You will need to use this name when viewing the migration status and progress in the task list.

3. Estimate the task size.

  ![](https://qcloudimg.tencent-cloud.cn/raw/0e2f9d5c9f184bb393275a60fa4d883b.png)

  We recommend you enter an optional accurate task size for us to better prepare resources.

4. Set the source of files to be migrated.
    Here, select **Alibaba Cloud OSS** for **Service Provider** and enter the `AccessKeyID` and `AccessKeySecret` of the Alibaba Cloud sub-account created above in **AccessKey** and **SecretKey** boxes respectively. Then, click the **Refresh** icon on the right of the **Migration bucket name** drop-down list to get the list of source buckets.
    ![](https://qcloudimg.tencent-cloud.cn/raw/f16ed6a2e72aa20f97245160115031b2.png)

  You can also manually enter a source bucket name.

  ![](https://qcloudimg.tencent-cloud.cn/raw/bf1d87d05a40055a8d0141336a84405c.png)

5. Select the header migration mode.
    If the file in the source bucket has headers and tags set and they need to be retained after migration, select to keep them or set the replacement rule.
    ![](https://qcloudimg.tencent-cloud.cn/raw/1bf638155d723024dfcc6146f2f222af.png)

6. Set the migration rule.
    Choose to migrate all the files of the specified bucket, or only migrate files with a specified prefix.
    ![](https://qcloudimg.tencent-cloud.cn/raw/0bd1276c60d8c33b43ab4f1f244eac1e.png)

7. Set a time range.
    Enable **Time Range** to migrate only files added or changed within the specified time range.
    ![](https://qcloudimg.tencent-cloud.cn/raw/0c9a0904eb75298494eb98817ae2bd9c.png)

8. Select a file storage type.
    Set the storage type of the migrated files based on your migration needs. You can select **Standard Storage**, **Infrequent Access Storage**, **Keep the original storage properties**, or **Archive Storage**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/0c7a24cd0b1a4531bd1d07351fc421fc.png)

9. Set the execution speed.
    All public cloud object storage services have speed limits. To ensure business stability, check with the source vendor and set the maximum available migration bandwidth in Mbps before migrating.
    ![](https://qcloudimg.tencent-cloud.cn/raw/59aab1e604aae6f72a4ea2fe2c334d94.png)

10. Select the migration target.
    In **Migration Target Information**, enter the `SecretId` and `SecretKey` of the Tencent Cloud sub-user for migration. Then, click the **Refresh** icon on the right of the **Migration bucket name** drop-down list to get the list of target buckets.
    ![](https://qcloudimg.tencent-cloud.cn/raw/4eae95aeaf3cd845286c9ef3d92ff030.png)

11. Specify the directory in the target bucket for migration and the method to process files with the same name.

     - **Save to the root directory**: Directly save the files in the source bucket to the target bucket's root directory while maintaining the original relative path.
     - **Save to the specified directory**: Save the files in the source bucket to the specified directory while maintaining the original relative path.
       ![](https://qcloudimg.tencent-cloud.cn/raw/5fa0fd94edbd4358a429b04b7ee6a766.png)
       For example:
       Two source bucket files `/a.txt` and `/dir/b.txt` are to be migrated, and "dest" is entered in the text box. In this case, after migration, the paths of these two files in the target bucket will be `/dest/a.txt` and `/dest/dir/b.txt`.
       If `dest/20180901` is entered in the text box, then after migration, the paths of these two files in the target bucket will be `/dest/20180901/a.txt` and `/dest/20180901/dir/b.txt`.

    >!
    >
    >- If you select **Overwrite** for files with the same name, the source files will directly overwrite the files with the same name in the target bucket.
    >- If you select **Skip** for files with the same name, the system will process them based on the last modification time of the files (`LastModified`):
    >  - If the `LastModified` of the file in the source address is at or after that of the file in the target address, overwriting will be performed.
    >  - If the `LastModified` of the file in the source address is before that of the file in the target address, no overwriting will be performed.
    >- Perform secondary migration if the object (file) content is changed during migration.

    

12. Select a migration mode.
     - **Create a migration task and download the Agent manually to start migration**: Select the Agent migration mode. After you click **Create and Start**, only the task configuration will be created. You must manually download the Agent and deploy it on the migration source server as instructed in [Using Semi-Managed Migration Agent](https://www.tencentcloud.com/document/product/1036/51593) to start the migration.
       ![](https://qcloudimg.tencent-cloud.cn/raw/92b3f400b8690ef9feb99ea1fc6bb6cb.png)

14. Click **Create and Start** to start the migration task.

![](https://qcloudimg.tencent-cloud.cn/raw/8de9b1313952da11cab45386021e5584.png)


## Viewing the Migration Status and Progress
You can view the status and progress of all file migration tasks on the file migration tool homepage:
•	For the **Task completed** status, green indicates that the migration task was completed and all files were successfully migrated, while yellow indicates that the migration task was completed but some files failed to be migrated.
•	After you click **Retry failed task**, files that failed in the task will be retried for migration, while files that have been successfully migrated will not be transferred again.
•	You can click **Export** to export the list of files that failed to be migrated.


## Estimating the File Migration Time
The migration speed is subject to the lowest speed during each stage of the migration process and is affected by factors such as the network transfer speed and maximum concurrency as detailed below:

| Affecting Factor | Description |
| ---------------------- | ------------------------------------------------------------ |
| Read speed of the migration source       | The read speed of the data source varies by vendor. <br><li>The transfer speed is generally 50–20,000 Mbps.<br><li>The file read QPS is generally 500–5,000 (the transfer of a large number of small files is subject to this concurrency). |
| Transfer speed of MSP     | MSP offers up to 2,000 Mbps migration bandwidth in fully managed mode. In semi-managed mode, the bandwidth is subject to your migration resource size. |
| Write speed of the migration target | COS: The default write speed is 15,000 Mbps, and the write QPS is 3,000–30,000. |



