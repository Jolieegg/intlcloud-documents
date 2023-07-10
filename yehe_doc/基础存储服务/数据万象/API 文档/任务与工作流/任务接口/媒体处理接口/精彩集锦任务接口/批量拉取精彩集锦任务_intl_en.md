## Feature Description
The API (`DescribeMediaJobs`) is used to pull jobs that meet specified conditions.

## Request

#### Sample request

```shell
GET /jobs?size=&states=&queueId=&startCreationTime=&endCreationTime= HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```


>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 



#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request does not have a request body.

#### Request parameters

The parameters are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:--|
|QueueId| None | ID of the queue from which jobs are pulled |String| Yes |
| Tag | None | Job type: VideoMontage | String | Yes |
| OrderByTime | None | `Desc` (default) or `Asc` | String | No |
| NextToken | None | Context token for pagination | String | No |
| Size | None | Maximum number of jobs that can be pulled. The default value is 10. The maximum value is 100. | Integer | No |
| States | None | Status of the jobs to pull. If you enter multiple job statuses, separate them by comma. <br>Valid values: All (default), Submitted, Running, Success, Failed, Pause, Cancel | String | No |
| StartCreationTime | None | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`. | String | No |
| EndCreationTime | None | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`.  | String | No |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

``` shell
<Response>
  <JobsDetail>
  </JobsDetail>
  <NextToken></NextToken>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| JobsDetail | Response | Job details. Same as `Response.JobsDetail` in `CreateMediaJobs`. |  Container |
| NextToken             | Response | Context token for pagination | String    |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).


## Samples

#### Request

```shell
GET /jobs?queueId=aaaaaaaaaaa&tag=VideoMontage HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 666
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>jabcxxxxfeipplsdfwe</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <StartTime></StartTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>VideoMontage<Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Output>
            <Region>ap-beijing</Region>
            <Bucket>abc-1250000000</Bucket>
            <Object>test-montage.mp4</Object>
        </Output>
    </Operation>
  </JobsDetail>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>jabcxxxxfeipplsdfwe</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <StartTime></StartTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>VideoMontage<Tag>
    <Input>
        <Object>test.mp4</Object>
    </Input>
    <Operation>
        <VideoMontage>
          <Container>
            <Format>mp4</Format>
          </Container>
          <Video>
            <Codec>H.264</Codec>
            <Bitrate>1000</Bitrate>
            <Width>1280</Width>
            <Height></Height>
          </Video>
          <Audio>
            <Codec>aac</Codec>
            <Samplerate>44100</Samplerate>
            <Bitrate>128</Bitrate>
            <Channels>4</Channels>
          </Audio>
          <Duration></Duration>
        </VideoMontage>
        <Output>
          <Region>ap-beijing</Region>
          <Bucket>abc-1250000000</Bucket>
          <Object>test-montage.gif</Object>
        </Output>
      </Operation>
  </JobsDetail>
</Response>
```


