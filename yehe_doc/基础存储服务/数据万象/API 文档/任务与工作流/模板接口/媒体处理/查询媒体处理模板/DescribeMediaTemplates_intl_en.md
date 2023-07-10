## Feature Description

This API is used to query a template.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateTranscodeTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer provides various capabilities such as online call, signature verification, SDK code generation, and quick API search. You can also use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>



## Request

#### Sample request

```shell
GET /template HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml
```

>?Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

The request body of this request is empty.

#### Request parameters

The parameters are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :------------------------------- | :------ | :--- |
| tag                | None     | Template tag. Default value: `All`.             | String  | No   |
| category           | None     | Valid values: `Official` (system preset template); `Custom` (custom template). Default value: `Custom`. | String  | No   |
| ids       | None | Template ID. If you enter multiple IDs, separate them by comma.  | String     | No |
| name          | None        | Template name prefix              | String     | No |
| pageNumber    | None        | Page number. Default value: `1`.                   | Integer     | No |
| pageSize    | None | Number of entries per page. Default value: `10`.                | Integer | No       |

Supported `tag` types are as follows:

| Template type | tag |
| :----------------- | :----- |
| Audio/Video transcoding         | Transcode |
| Video-to-animated image conversion          | Animation |
| Screenshot            | Snapshot |
| Audio/Video splicing          | Concat |
| Voice/Sound separation            | VoiceSeparate |
| Video montage            | VideoMontage |
| Video enhancement            | VideoProcess |
| Super resolution          | SuperResolution |
| Image/Text watermark       | Watermark |
| Text to speech            | Tts |
| Professional audio/video transcoding       | TranscodePro |
| Top speed codec transcoding            | HighSpeedHd |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

``` shell
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TemplateList>
        <TemplateId>A</TemplateId>
        <Name>TemplateName</Name>
        <Tag>Transcode</Tag>
        <TransTpl>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Profile>high</Profile>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Fps>30</Fps>
                <Preset>medium</Preset>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
            </Audio>
            <TransConfig>
                <AdjDarMethod>scale</AdjDarMethod>
                <IsCheckReso>false</IsCheckReso>
                <ResoAdjMethod>1</ResoAdjMethod>
            </TransConfig>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </TransTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </TemplateList>
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
| TotalCount         | Response | Total number of templates                       | Int       |
| PageNumber         | Response | Current page number, which is the same as `pageNumber` in the request.                           | Int       |
| PageSize           | Response | Number of entries per page, which is the same as `pageSize` in the request.   | Int       |
| TemplateList       | Response | Template array                       | Container array |

For different types of templates, the `TemplateList` content is the same as the `Response` of the corresponding template creation API. For more information, see:
- <a href="https://intl.cloud.tencent.com/document/product/1045/49911" target="_blank">Creating Audio/Video Transcoding Template</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49906" target="_blank">Creating Animated Image Template</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49909" target="_blank">Creating Screenshot Template</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49907" target="_blank">Creating Splicing Template</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49916" target="_blank">Creating Voice/Sound Separation Template</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49914" target="_blank">Creating Video Montage Template</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49915" target="_blank">Creating Video Enhancement Template</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49910" target="_blank">Creating Super Resolution Template</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49917" target="_blank">Creating Watermark Template</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49913" target="_blank">Creating Text-to-Speech Template</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49912" target="_blank">Creating Professional Transcoding Template</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49908" target="_blank">Creating Top Speed Codec Transcoding Template</a>

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

**Sample 1. Querying by template ID**

#### Request

```shell
GET /template?ids=t1847cd4ca57f543e89f551dbe68169eb9,t1a30a323f55434a29b25bf2a16bdf5f59,C HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <TemplateList>
        <TemplateId>t1847cd4ca57f543e89f551dbe68169eb9</TemplateId>
        <Name>TemplateName</Name>
        <Tag>Transcode</Tag>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <TransTpl>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Profile>high</Profile>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Fps>30</Fps>
                <Preset>medium</Preset>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
            </Audio>
            <TransConfig>
                <AdjDarMethod>scale</AdjDarMethod>
                <IsCheckReso>false</IsCheckReso>
                <ResoAdjMethod>1</ResoAdjMethod>
            </TransConfig>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </TransTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </TemplateList>
    <TemplateList>
        <TemplateId>t140325e8918ac423da53b7d78dbbab564</TemplateId>
        <Name>template_name3544697</Name>
        <Tag>Concat</Tag>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <ConcatTemplate>
            <ConcatFragment>
                <Mode>Start</Mode>
                <Url>https://test-1234567890.cos.ap-chongqing.myqcloud.com/input/ad.mp4</Url>
            </ConcatFragment>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate/>
                <Bitrate/>
                <Channels/>
                <Remove>false</Remove>
            </Audio>
            <Video>
                <Codec>H.264</Codec>
                <Width>1280</Width>
                <Height>960</Height>
                <Fps>15</Fps>
                <Remove>false</Remove>
                <Crf>25</Crf>
            </Video>
            <Container>
                <Format>mp4</Format>
            </Container>
            <DirectConcat>false</DirectConcat>
        </ConcatTemplate>
        <CreateTime>2022-06-29T14:37:44+0800</CreateTime>
        <UpdateTime>2022-06-29T14:37:44+0800</UpdateTime>
    </TemplateList>
    <NonExistTIDs>
        <TemplateId>C</TemplateId>
    </NonExistTIDs>
</Response>
```

**Sample 2. Querying by paginated list**

#### Request

```shell
GET /template?pageSize=10&pageNumber=1 HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <TotalCount>2</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TemplateList>
        <TemplateId>t1847cd4ca57f543e89f551dbe68169eb9</TemplateId>
        <Name>TemplateName</Name>
        <Tag>Transcode</Tag>
        <TransTpl>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Profile>high</Profile>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Fps>30</Fps>
                <Preset>medium</Preset>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
            </Audio>
            <TransConfig>
                <AdjDarMethod>scale</AdjDarMethod>
                <IsCheckReso>false</IsCheckReso>
                <ResoAdjMethod>1</ResoAdjMethod>
            </TransConfig>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </TransTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </TemplateList>
    <TemplateList>
        <TemplateId>t140325e8918ac423da53b7d78dbbab564</TemplateId>
        <Name>template_name3544697</Name>
        <Tag>Concat</Tag>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <ConcatTemplate>
            <ConcatFragment>
                <Mode>Start</Mode>
                <Url>https://test-1234567890.cos.ap-chongqing.myqcloud.com/input/ad.mp4</Url>
            </ConcatFragment>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate/>
                <Bitrate/>
                <Channels/>
                <Remove>false</Remove>
            </Audio>
            <Video>
                <Codec>H.264</Codec>
                <Width>1280</Width>
                <Height>960</Height>
                <Fps>15</Fps>
                <Remove>false</Remove>
                <Crf>25</Crf>
            </Video>
            <Container>
                <Format>mp4</Format>
            </Container>
            <DirectConcat>false</DirectConcat>
        </ConcatTemplate>
        <CreateTime>2022-06-29T14:37:44+0800</CreateTime>
        <UpdateTime>2022-06-29T14:37:44+0800</UpdateTime>
    </TemplateList>
</Response>
```
