## Overview

This document provides an overview of APIs and SDK code samples related to COS inventory.

| API | Operation Name | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Creating an inventory job | Creates an inventory job for a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries the inventory jobs of a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job from a bucket |


## Creating an Inventory Job

#### API description

This API is used to create an inventory job for a bucket. For more information, see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

> !
> - Up to 1,000 inventory jobs can be created in one COS bucket.
> - You must add a bucket policy to the destination bucket in order for COS to write the output file of the inventory job to the destination bucket.
> - To call this API, make sure that you have the necessary permission for bucket inventory jobs; the bucket owner has this permission by default. If you do not have it, you should request it from the bucket owner first. 


#### Request samples

Sample 1. Creating an inventory job with server-side encryption.

[//]: # (.cssg-snippet-put-bucket-inventory)
```js
cos.putBucketInventory({
    Bucket: 'sourcebucket-1250000000',  /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Id: 'inventory_test',               /* Required */
    InventoryConfiguration: {
        Id: 'inventory_test',
        IsEnabled: 'true',
        Destination: {
            COSBucketDestination: {
                Format: 'CSV',
                AccountId: '100000000001',
                Bucket: 'qcs::cos:ap-beijing::targetbucket-1250000000',
                Prefix: 'inventory_test_prefix',
                Encryption: {
                    SSECOS: ''
                }
            }
        },
        Schedule: {
            Frequency: 'Daily'
        },
        Filter: {
            Prefix: 'filter_prefix'
        },
        IncludedObjectVersions: 'All',
        OptionalFields: [
            'Size',
            'LastModifiedDate',
            'StorageClass',
            'ETag'
        ]
    }
}, function(err, data) {
    console.log(err || data);
});
```

Sample 2. Creating an inventory job without server-side encryption.

```js
cos.putBucketInventory({
    Bucket: 'sourcebucket-1250000000',  /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Id: 'inventory_test',       /* Required */
    InventoryConfiguration: {
        Id: 'inventory_test',
        IsEnabled: 'true',
        Destination: {
            COSBucketDestination: {
                Format: 'CSV',
                AccountId: '100000000001',
                Bucket: 'qcs::cos:ap-beijing::targetbucket-1250000000',
                Prefix: 'inventory_test_prefix'
            }
        },
        Schedule: {
            Frequency: 'Daily'
        },
        Filter: {
            Prefix: 'filter_prefix'
        },
        IncludedObjectVersions: 'All',
        OptionalFields: [
            'Size',
            'LastModifiedDate',
            'StorageClass',
            'ETag'
        ]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Name of the bucket for which the inventory job is configured in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Id | ID of the inventory job.<br>Default: None<br>Valid characters: `a-z，A-Z，0-9，-，_，.`                               | String      | Yes   |
| InventoryConfiguration | Inventory configuration parameters                               | Object      | Yes   |
| - Id | ID of the inventory job.<br>Default: None<br>Valid characters: `a-z，A-Z，0-9，-，_，.`                               | String      | Yes   |
| - IsEnabled             | Indicates whether inventory is enabled.<br><li>`true` indicates it is enabled<br><li>`false` indicates no inventory list will be generated.                                           | String      | Yes   |
| - IncludedObjectVersions | Indicates whether to include object versions in the inventory<br><li>If this is set to `All`, the inventory will include all object versions and the additional fields `VersionId`, `IsLatest`, and `DeleteMarker`.<br><li>If this is set to `Current`, no object versions will be included in the inventory. | String | Yes |
| - Filter             | Filters the objects subject to the inventory job with the prefix specified in this parameter                                           | Object      | No   |
| - - Prefix | Prefix of the objects to be inventoried | String | No |
| - OptionalFields | Optional fields included in the inventory result, including Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus | Array | No |
| - Schedule             | Schedule for the inventory job                                           | Object      | Yes   |
| - - Frequency             | Frequency of the inventory job. Enumerated values: Daily, Weekly                                           | String      | Yes   |
| - Destination             | Destination that stores the inventory results                                           | Object      | Yes   |
| - - COSBucketDestination             | Destination bucket that stores the exported inventory results                                           | Object      | Yes   |
| - - - Bucket             | Name of the bucket that stores the inventory results                                           | String      | Yes   |
| - - - AccountId             | ID of the bucket owner, e.g. 100000000001                                           | String      | No   |
| - - - Prefix             | The prefix for inventory reports to deliver. COS automatically adds a '/' after the prefix you specify.<br>For example, if you specify 'Prefix' as the prefix, COS will deliver inventory reports to the path `Prefix/inventory_report`.                                           | String      | No   |
| - - - Format             | Format of the inventory results. Value: CSV                                           | String      | Yes   |
| - - - Encryption             | The option of enabling server-side encryption for inventory results                                           | Object      | No   |
| - - - - SSECOS             | Encryption with a COS-managed key. Left empty.                                           | String      | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Returns a network or service error when the request fails. If the request is successful, this is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Returns data when the request is successful. If the request fails, this is empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |

## Querying Inventory Jobs

#### API description

This API is used to query the inventory jobs of a bucket. To initiate this request, you need to provide the inventory job ID, and a request signature that indicates that the request has been permitted. For more information, see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

> !
> - To call this API, make sure that you have the necessary permission for bucket inventory jobs.
> - The bucket owner has such permission by default. If you do not have the permission, you can request it from the bucket owner.  

#### Sample request 

[//]: # (.cssg-snippet-get-bucket-inventory)
```js
cos.getBucketInventory({
    Bucket: 'sourcebucket-1250000000',  /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Id: 'inventory_test'                /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

```json
{
    "InventoryConfiguration": {
        "Id":"inventory_test",
        "IsEnabled":"true",
        "Destination":{
            "COSBucketDestination": {
                "Format":"CSV",
                "AccountId":"100000000001",
                "Bucket":"qcs::cos:ap-beijing::targetbucket-1250000000",
                "Prefix":"inventory_test_prefix",
                "Encryption": {
                    "SSECOS":""
                }
            }
        },
        "Schedule": {
            "Frequency":"Daily"
        },
        "Filter": {
            "Prefix":"filter_prefix"
        },
        "IncludedObjectVersions":"All",
        "OptionalFields": [
            "Size",
            "LastModifiedDate",
            "StorageClass",
            "ETag"
        ]
    }
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Name of the bucket for which the inventory job is queried in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Id | ID of the inventory job.<br>Default: None<br>Valid characters: `a-z，A-Z，0-9，-，_，.`                               | String      | Yes   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Returns a network or service error when the request fails. If the request is successful, this is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | Returns an HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Returns headers | Object |
| data | Returns data when the request is successful. If the request fails, this is empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| - InventoryConfiguration | Inventory configuration parameters                               | Object      |
| - - Id | ID of the inventory job.<br>Default: None<br>Valid characters: `a-z，A-Z，0-9，-，_，.`                               | String      |
| - - IsEnabled             | Indicates whether inventory is enabled.<br><li>`true` indicates it is enabled<br><li>`false` indicates no inventory list will be generated.                                           | String      |
| - - IncludedObjectVersions | Indicates whether to include object versions in the inventory<br><li>If this is set to `All`, the inventory will include all object versions and the additional fields `VersionId`, `IsLatest`, and `DeleteMarker`.<br><li>If this is set to `Current`, no object versions will be included in the inventory. | String |
| - - Filter             | Filters objects subject to the inventory job with the prefix specified in this field                                           | Object      |
| - - - Prefix | Prefix of the objects to be inventoried | String |
| - - OptionalFields | Optional fields included in the inventory result, including Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus | Array |
| - - Schedule             | Schedule for the inventory job                                           | Object      | 
| - - - Frequency             | Frequency of the inventory job. Enumerated values: Daily, Weekly                                           | String      |
| - - Destination             | Destination that stores the inventory results                                           | Object      |
| - - - COSBucketDestination             | Destination bucket that stores the exported inventory results                                           | Object      |
| - - - - Bucket             | Name of the bucket that stores the inventory results                                           | String      |
| - - - - AccountId             | ID of the bucket owner, e.g. 100000000001                                           | String      |
| - - - - Prefix             | The prefix for inventory reports to deliver. COS automatically adds a '/' after the prefix you specify.<br>For example, if you specify 'Prefix' as the prefix, COS will deliver inventory reports to the path `Prefix/inventory_report`.                                           | String      |
| - - - - Format             | Format of the inventory results. Value: CSV                                           | String      |
| - - - - Encryption             | The option of enabling server-side encryption for inventory results                                           | Object      |
| - - - - - SSECOS             | Encryption with a COS-managed key. Left empty.                                           | String      |

## Deleting an Inventory Job

#### API description

This API is used to delete an inventory job from a bucket with the inventory job ID you specify.
For more information, please see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

> !
> - To call this API, make sure that you have the necessary permission for bucket inventory jobs.
> - The bucket owner has such permission by default. If you do not have the permission, you can request it from the bucket owner.

#### Sample request 

[//]: # (.cssg-snippet-delete-bucket-inventory)
```js
cos.deleteBucketInventory({
    Bucket: 'sourcebucket-1250000000',  /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Id: 'inventory_test'                /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Name of the bucket from which the inventory job is deleted in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Id | ID of the inventory job. Default: None<br/>Valid characters: `a-z，A-Z，0-9，-，_，.`                               | String      | Yes   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Returns a network or service error when the request fails. If the request is successful, this is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Returns data when the request is successful. If the request fails, this is empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
