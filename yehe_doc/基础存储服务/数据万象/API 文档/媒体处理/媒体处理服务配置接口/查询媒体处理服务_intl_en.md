## Feature Description

This API (`DescribeMediaBuckets`) is used to query buckets with media processing enabled.

## Request

#### Sample request

```shell
GET /mediabucket HTTP/1.1
Host: ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/49351).

#### Request body

The request body of this request is empty.

#### Request parameters



| Parameter | Description | Type | Required |
| :---------- | :----- | :------------------ | :------- |
| regions     |  Region information, such as `ap-shanghai` and `ap-beijing`. To specify multiple regions, separate them by comma. For more information, see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423). | string |  No    |
| bucketNames | Bucket name. To specify multiple bucket names, separate them by comma. Exact search is supported. | string | No |
| bucketName  | Bucket name prefix for prefix search.        | string |  No       |
| pageNumber  | Page number.                  |  string | No       |
| pageSize    | Number of entries per page.                | string | No       |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49352).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <MediaBucketList>
        <BucketId></BucketId>
        <Region></Region>
        <CreateTime></CreateTime>
    </MediaBucketList>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------------------------ | :-------- |
| RequestId          | Response | Unique ID of the request.                   | String    |
| TotalCount         | Response | Total number of media buckets.                | Int       |
| PageNumber         | Response | Current page number, which is the same as `pageNumber` in the request.                           | Int       |
| PageSize           | Response | Number of entries per page, which is the same as `pageSize` in the request.   | Int       |
| MediaBucketList    | Response | Media bucket list.                | Container |

`MediaBucketList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------- | :---------------------- | :----- |
| BucketId           | Response.MediaBucketList | Bucket ID.               | String |
| Name               | Response.MediaBucketList | Bucket name, which is the same as `BucketId`. | String |
| Region             | Response.MediaBucketList | Bucket region.              | String |
| CreateTime         | Response.MediaBucketList | Creation time.                | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request

```shell
GET /mediabucket HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: ci.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****



<Response>
      <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
      <TotalCount>1</TotalCount>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <MediaBucketList>
            <BucketId></BucketId>
            <Region></Region>
            <CreateTime></CreateTime>
      </MediaBucketList>
      <MediaBucketList>
            <BucketId></BucketId>
            <Region></Region>
            <CreateTime></CreateTime>
      </MediaBucketList>
</Response>
```
