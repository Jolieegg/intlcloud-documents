## 概述

对象存储内容审核服务提供了图片、视频、音频、文本、文档、网页等多媒体的内容安全智能审核服务，可帮助用户有效识别色情低俗、违法违规、恶心反感等违禁内容，规避运营风险。目前可支持以下类型的文件格式进行内容审核：

| 文件类型 | 规格限制                                                     |
| -------- | ------------------------------------------------------------ |
| 图片     | <ul  style="margin: 0;"><li>支持 png、jpeg、jpg、bmp、webp、gif 格式。</li><li>图片大小不超过5MB。图片宽高不低于20 x 20像素。</li></ul> |
| 视频     | <ul  style="margin: 0;"><li>支持 mp4、avi、mkv、wmv、rmvb、flv、m3u8 格式。</li><li>视频大小不能超过5GB，截帧数不能超过1万帧。</li></ul> |
| 音频     | <ul  style="margin: 0;"><li>音频格式：当前支持 mp3、wav、aac、flac、amr、3gp、m4a、wma、ogg、ape。</li><li>音频码率：128Kbps-256Kbps。<li>音频大小：文件小于600MB。最大时长：3小时。</li></ul> |
| 文本     | 支持 html、 txt 格式，且文件大小不超过1MB。                  |
| 直播     | <ul  style="margin: 0;"><li>直播流时长支持：5小时以内。</li><li>支持的直播流媒体协议：rmtp、hls、http、https 等主流协议。</li></ul>     |
| 文档     | 通过文档处理服务将文档转换为图片进行审核，目前支持 pdf、ppt、excel 等几十种文档格式。详见 [文档预览概述](https://intl.cloud.tencent.com/document/product/436/49159)。 |
| 网页     | 支持对网页文件进行自动检测，从 OCR 文本识别、物体检测（实体、广告台标、二维码等）、图像识别几个维度，通过深度学习技术，识别网页中的违规内容。 |


>? 内容审核为收费项，由数据万象收取。
>

![](https://staticintl.cloudcachetci.com/yehe/backend-news/Exni357_PRELIM__%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US.png)

开通审核服务后，您可以实现以下操作：

- 配置自动审核，对上传到存储桶中的数据进行自动审核，并自动冻结违规数据
- 调用接口对第三方数据进行审核
- 对存储桶中的历史数据进行一次性批量审核

## 适用场景

适用于社交、电商、广告、游戏等领域。可对上述类型的文件进行审核，审核类型包括涉黄、违法违规及广告传播。

## 地域限制

支持地域如下：

| 地域 | 地域简称     |
| :--- | :----------- |
| 北京 | ap-beijing   |
| 南京 | ap-nanjing   |
| 上海 | ap-shanghai  |
| 广州 | ap-guangzhou |
| 成都 | ap-chengdu   |
| 重庆 | ap-chongqing |

如有您希望在其他地域使用内容审核功能，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们。

## 使用方法

### 使用对象存储控制台

#### 自动审核

您可以通过在对象存储控制台开启自动审核服务，对新上传的图片、视频、音频、文件、文档、网页进行自动审核，详情请参见 [自动审核](https://www.tencentcloud.com/document/product/436/52097)。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/3YaP402_PRELIM__%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)


#### 历史数据审核

您可以通过对象存储控制台开启历史数据审核服务，对存储桶中已有的图片、视频、音频、文本、文档、网页进行一次性的批量审核。

### 使用 API 接口

您可以使用我们提供的 API 接口对图片、视频、音频、文本、文档、网页进行内容审核，详情请参见以下 API 文档：

- [图片审核](https://intl.cloud.tencent.com/document/product/436/48537) 
- [视频审核](https://intl.cloud.tencent.com/document/product/436/48249) 
- [音频审核](https://intl.cloud.tencent.com/document/product/436/48262)
- [文本审核](https://www.tencentcloud.com/document/product/436/48187)
- [文档审核](https://www.tencentcloud.com/document/product/436/48257)
- [网页审核](https://www.tencentcloud.com/document/product/436/48281)
- [直播审核](https://www.tencentcloud.com/document/product/436/48276)

对于审核结果为敏感的数据，我们建议您可以选择以下几种方式之一进行处理：
- 修改文件访问权限为私有读，杜绝用户在公网匿名访问，修改权限接口请参考 [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748)。
- 将文件移动至备份目录，移动文件是通过将原文件拷贝到指定目录后再删除原文的方式实现的，接口请参考 [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) 和 [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)。
- 删除文件，接口请参考 [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)。


