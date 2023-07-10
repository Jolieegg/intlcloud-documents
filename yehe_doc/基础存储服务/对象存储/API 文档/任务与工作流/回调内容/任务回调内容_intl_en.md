## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request whose body contains notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
       <JobsDetail>
           <Code></Code>
           <Message></Message>
           <JobId></JobId>
           <State></State>
           <CreationTime></CreationTime>
           <EndTime></EndTime>
           <QueueId></QueueId>
           <Tag></Tag>
           <Input>
                 <CosHeaders></CosHeaders>
                 <Region></Region>
                 <BucketId></BucketId>
                 <Object></Object>
           </Input>
           <Operation>
                 <TemplateId></TemplateId>
                 <TemplateName></TemplateName>
                 <MediaResult></MediaResult>
                 <Output>
                    <Region></Region>
                    <Bucket></Bucket>
                    <Object></Object>
                 </Output>
                 <MediaInfo>
                 </MeidaInfo>
           </Operation>
           <Workflow>   
                 <RunId></RunId>   
                 <WorkflowId></WorkflowId>  
                 <WorkflowName></WorkflowName>  
                 <Name></Name>
           </Workflow>
       </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| JobsDetail         | Response | Job details | Container |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :------------------------------------- | :-------- |
| Code               | Response.JobsDetail | Error code, which is meaningful only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error description, which is meaningful only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag                | Response.JobsDetail | Job type                              | String    |
| State              | Response.JobsDetail | Job status. Valid values: Success, Failed | String    |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| EndTime            | Response.JobsDetail | Job end time                         | String    |
| QueueId            | Response.JobsDetail | Queue ID of the job                       | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation          | Response.JobsDetail | Operation rule                           | Container |
| Workflow | Response.JobsDetail | Workflow information of the job |  Container |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------ | :----------------------------------------------------------- | :-------- |
| CosHeaders         | Response.JobsDetail.Input | Custom header information of the input file in array format. There can be multiple headers. This node is included only for workflow-triggered jobs. | Container |
| Object             | Response.JobsDetail.Input | Name of the input file, i.e., object key (ObjectKey) in COS                               | String    |
| Region             | Response.JobsDetail.Input | Region of the input bucket                                | String    |
| BucketId           | Response.JobsDetail.Input | ID of the input bucket                                 | String    |

`CosHeaders` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------- | :------------------ | :----- |
| Key                | Response.JobsDetail.Input.CosHeaders | Name of the custom header  | String |
| Value              | Response.JobsDetail.Input.CosHeaders | Value of the custom header | String |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :------------------------------- | :-------- |
| TemplateId         | Response.JobsDetail.Operation | Job template ID                     | String    |
| TemplateName | Response.JobsDetail.Operation | Job template name |  String |
| Output             | Response.JobsDetail.Operation | File output address               | Container |
| MediaResult        | Response.JobsDetail.Operation | Job output information                   | Container |
| MediaInfo          | Response.JobsDetail.Operation | Transcoding output video information. This node will not be returned when there is no output video. | Container |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------ | :--------------- | :----- |
| Region             | Response.Operation.Output | Bucket region     | String |
| Bucket             | Response.Operation.Output | Result storage bucket | String |
| Object             | Response.Operation.Output | Result filename | String |

`MediaResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :----------------- | :-------- |
| OutputFile         | Response.Operation.MediaResult | Information of the actual output file | Container |

`OutputFile` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------------------- | :------------------------------------- | :----- |
| Region             | Response.Operation.MediaResult.OutputFile | Bucket region                          | String |
| Bucket             | Response.Operation.MediaResult.OutputFile | Result storage bucket                       | String |
| ObjectPrefix       | Response.Operation.MediaResult.OutputFile | Output filename prefix                         | String |
| ObjectName         | Response.Operation.MediaResult.OutputFile | List of output filenames in array format | String |

>! The actual output file is the `StringConcat(ObjectPrefix,ObjectName)` file in the bucket specified by `Bucket` in the region specified by `Region`.
>

`Workflow` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ----------------------------------------- | -------------------------------------- | ------ |
| RunId              | Response.Workflow | Workflow instance ID                    | String |
| WorkflowId         | Response.Workflow | Workflow ID                       | String |
| WorkflowName       | Response.Workflow | Workflow name                      | String |
| Name               | Response.Workflow | Workflow node name                   | String |


`MediaInfo` has the following sub-nodes:
Same as the `Response.MediaInfo` node in the `GenerateMediaInfo` API.

## Use Cases

```plaintext
<Response>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2020-11-16T16:43:29+0800</CreationTime>
        <EndTime>2020-11-16T16:43:33+0800</EndTime>
        <Input>
            <CosHeaders>
                <Key>x-cos-meta-test</Key>
                <Value>testvalue</Value>
            </CosHeaders>
            <CosHeaders>
                <Key>x-cos-meta-name</Key>
                <Value>xxxxxx</Value>
            </CosHeaders>
            <CosHeaders>
                <Key>x-cos-meta-age</Key>
                <Value>10</Value>
            </CosHeaders>
            <Object>1/2/3/4/5/xxx.mp4</Object>
            <Region>ap-beijing</Region>
            <BucketId>examplebucket-1250000000</BucketId>
        </Input>
        <JobId>jccddc41c27e711ebbff5874bc5b36868</JobId>
        <Message/>
        <Operation>
            <MediaResult>
                <OutputFile>
                    <Bucket>examplebucket-1250000000</Bucket>
                    <Md5Info>
                        <Md5>39ad161a7807240f4d6f94767e8e2f89</Md5>
                        <ObjectName>1/2/Conversion to MP4-xxx_iccba81fa27e711eb989d525400276c76.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>1/2/Conversion to MP4-xxx_iccba81fa27e711eb989d525400276c76.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>examplebucket-1250000000</Bucket>
                <Object>1/2/Conversion to mp4-xxx_iccba81fa27e711eb989d525400276c76.${ext}</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t182c0ca7d91ca40969a3fc97c5559091a</TemplateId>
            <TemplateName>example</TemplateName>
        </Operation>
        <Workflow>   
            <RunId>rccddc41c27e711ebbff5874bc5b36868</RunId>   
            <WorkflowId>wccddc41c27e711ebbff5874bc5b36868</WorkflowId>  
            <WorkflowName>workflow</WorkflowName>  
            <Name>Transcode_1600413767444</Name>
        </Workflow>
        <QueueId>p791b0bca54ee44289f0d4b1d90796c4f</QueueId>
        <State>Success</State>
        <Tag>Transcode</Tag>
    </JobsDetail>
</Response>
```
