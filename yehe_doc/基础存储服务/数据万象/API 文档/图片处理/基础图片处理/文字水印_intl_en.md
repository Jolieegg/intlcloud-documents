## Feature Overview
CI uses the **watermark** API to add text watermarks in real time. An input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, its total number of pixels (Width x Height x Number of frames) cannot exceed 250 million.

An image can be processed:

- Upon download
- Upon upload
- In cloud

## API Format

#### 1. Processing upon download

```plaintext
GET /<ObjectKey>?watermark/2/text/<encodedText>
                            /font/<encodedFont>
                            /fontsize/<fontSize>
                            /fill/<encodedColor>
                            /dissolve/<dissolve>
                            /gravity/<gravity>
                            /dx/<dx>
                            /dy/<dy>
                            /batch/<type>
                            /degree/<degree>
                            /shadow/<shadow> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

>? Spaces and line breaks above are for readability only and can be ignored.

#### 2. Processing upon upload

```plaintext
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: 
{
  "is_pic_info": 1,
  "rules": [{
      "fileid": "exampleobject",
      "rule": "watermark/2/text/<encodedText>
                        /font/<encodedFont>
                        /fontsize/<fontSize>
                        /fill/<encodedColor>
                        /dissolve/<dissolve>
                        /gravity/<gravity>
                        /dx/<dx>
                        /dy/<dy>
                        /batch/<type>
                        /degree/<degree>
                        /shadow/<shadow>"
  }]
}
```

>? `Pic-Operations` is a JSON string. Its parameters are as described in [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695).
>

#### 3. Processing in-cloud data

```plaintext
POST /<ObjectKey>?image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: 
{
  "is_pic_info": 1,
  "rules": [{
      "fileid": "exampleobject",
      "rule": "watermark/2/text/<encodedText>
                        /font/<encodedFont>
                        /fontsize/<fontSize>
                        /fill/<encodedColor>
                        /dissolve/<dissolve>
                        /gravity/<gravity>
                        /dx/<dx>
                        /dy/<dy>
                        /batch/<type>
                        /degree/<degree>
                        /shadow/<shadow>"
  }]
}
```


>? 
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 



## Parameters

In the code above, `watermark` is the operation name and the number `2` indicates that the watermark is a text.

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           |
| /text/  | Watermark text, which must be [URL-safe Base64-encoded](https://intl.cloud.tencent.com/document/product/1045/33430) |
| /font/ | Font of the text, which must be [URL-safe Base64-encoded](https://intl.cloud.tencent.com/document/product/1045/33430). Default font: Tahoma.ttf (see [Supported Fonts](https://intl.cloud.tencent.com/document/product/1045/40681)). |
| /fontsize/   | Font size, in pt. Default value: 13. To scale the text watermark proportionally based on the original image, convert the text watermark to a PNG image. For more configuration information, see [Image Watermarking](https://intl.cloud.tencent.com/document/product/1045/33720).                     |
| /fill/ | Font color. The value must be in hexadecimal format, for example, `#FF0000`. For format conversion, see [RGB Color Codes Chart](https://www.rapidtables.com/web/color/RGB_Color.html). The value must be [URL-safe Base64-encoded](https://intl.cloud.tencent.com/document/product/1045/33430). Default value: `#3D3D3D` (gray). |
| /dissolve/ | Text opacity. Value range: 1−100. Default value: `90` (meaning 90% opacity) |
| /gravity/    | Position of the text watermark, which is a square in a [3x3 grid](#1). Default value: `southeast` |
| /dx/ | Horizontal offset in pixels. Default value: `0` |
| /dy/ | Vertical offset in pixels. Default value: `0` |
| /batch/ | Whether to tile the text watermark. If this parameter is set to `1`, the text watermark will be tiled across the input image. |
| /degree/ | Angle to rotate text watermarks. This parameter is valid only when `/batch/` is set to `1`. Value range: 0−360. Default value: `0`  |
| /shadow/| Text shadow effect. Value range: 0−100. Default value: `0`, indicating no shadow.   |   


<span id="1"></span>
## 3x3 Grid Position Diagram

The 3x3 grid position diagram is as follows. Once you specify the `gravity` parameter for an operation, the corresponding red dot becomes the reference point, and offsets will be relative to this point.
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>!
> - If `gravity` is set to `center`, `dx` and `dy` are invalid.
> - If `gravity` is set to `north` or `south`, `dx` is invalid.
> - If `gravity` is set to `west` or `east`, `dy` is invalid.

## Examples

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695) and use **Processing upon upload** or **Processing in-cloud data**.
>


#### Example 1: Adding a text watermark

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/2/text/6IW-6K6v5LqRwrfkuIfosaHkvJjlm74/fill/IzNEM0QzRA/fontsize/20/dissolve/50/gravity/northeast/dx/20/dy/20/batch/1/degree/45
```

After text watermarks are added:
![](https://main.qcloudimg.com/raw/e2ea173afafb7b50a2a7824b9173edf2.jpeg)

#### Example 2: Adding a text watermark with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&).

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&watermark/2/text/6IW-6K6v5LqRwrfkuIfosaHkvJjlm74/fill/IzNEM0QzRA/fontsize/20/dissolve/50/gravity/northeast/dx/20/dy/20/batch/1/degree/45
```

>? You can get the value of `<signature>` as instructed in [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple example for your reference (it might have expired or become inaccessible). For more information, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```

