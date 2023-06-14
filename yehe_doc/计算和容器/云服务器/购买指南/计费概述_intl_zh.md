您可直接使用 [CVM 价格计算器](https://buy.tencentcloud.com/price/cvm/calculator) 查看您所需的各个产品的组合价格，估算资源成本。将所需产品添加至购买预算清单，更可实现一键购买。

<dx-alert infotype="notice" title="">
为保证获取到的价格的准确性，请您登录后查看。
</dx-alert>

## 计费模式

腾讯云提供三种类型的云服务器购买方式：预留实例、按量计费和竞价实例，分别适用于不同场景下的用户需求，详情可参考 [计费模式](https://www.tencentcloud.com/document/product/213/2180)。

## 实例

实例决定了用于实例的主机硬件配置，每一个实例类型提供不同的计算和存储能力，您可以基于需要提供的服务规模而选择实例计算能力、存储空间和网络访问方式。
根据底层硬件的不同，腾讯云目前提供了丰富的机型规格，具体详情可参见 [实例规格](https://intl.cloud.tencent.com/document/product/213/11518)。

关于不同实例类型价格，可参见 [实例计费模式](https://intl.cloud.tencent.com/document/product/213/2180)。

## 存储

腾讯云为云服务器实例提供了不同类型的灵活、经济且易于使用的数据存储设备。不同的存储设备具有不同的性能和价格，适用于不同的使用场景。存储依据不同的维度来划分，可以分成以下几种：
- 按使用场景不同，分为系统盘和数据盘。
- 按架构模式不同，分为云硬盘、本地盘和对象存储。

目前腾讯云提供多种[云硬盘类型](https://www.tencentcloud.com/document/product/362/31636)：高性能云硬盘、通用型SSD云硬盘、 SSD 云硬盘、增强型SSD云硬盘、极速型SSD云硬盘。计费模式分为包年包月、按量计费、竞价实例。
关于硬盘价格的详细信息，可参见 [硬盘价格总览](https://intl.cloud.tencent.com/document/product/213/2255)。

## 网络带宽

腾讯云提供的任何网络类型的运营商接入均为 BGP 多线路，保证线路质量。目前网络提供按流量与按带宽两种网络计费方式。
- 按带宽计费：按公网传输速率（单位为 Mbps）计费，当您的带宽利用率高于10%时，可以考虑优先选择按带宽计费。
- 按流量计费：按公网传输的数据总量（单位为 GB）计费，当您的带宽利用率低于10%时，可以考虑优先选择按流量计费。

关于各种网络带宽计费模式的详细信息，可参见 [公网计费模式](https://intl.cloud.tencent.com/document/product/213/10578)。


## 镜像[](id:mirrorBilling)
使用镜像可能会产生一定的费用，各类型镜像费用说明如下，详细信息请参见： [镜像计费说明](https://www.tencentcloud.com/document/product/213/55134)。
<table>
<tr>
<th width="16%">镜像类型</th><th>说明</th>
</tr>
<tr>
<td>公共镜像</td>
<td>包含开源镜像及商业镜像。
<ul style="margin:0px">
<li>开源镜像不产生 License 许可费用。</li>
<li>商业镜像会产生一定的 License 许可费用，请以实际下单时为准。
</li>
</ul>
</td>
</tr>
<tr>
<td>自定义镜像</td>
<td>
计费包含以下两部分：
<ul style="margin:0px">
<li>快照费用：由于镜像底层使用了云硬盘快照服务，保留自定义镜像会产生一定的快照费用。国内地域提供80GB的 <a href="https://intl.cloud.tencent.com/document/product/362/32415">赠送额度</a>，超额后将按容量计费，详情请参见 <a href="https://intl.cloud.tencent.com/document/product/362/32415">快照计费概述</a>。</li>
<li>镜像费用：若自定义镜像的最终来源为付费镜像，且您使用了该自定义镜像，则需要收取镜像费用。</li>
</ul>
</td>
</tr>
<tr>
<td>共享镜像</td>
<td>共享镜像是将创建好的自定义镜像分享给其他腾讯云账户的镜像。若该镜像最终来源为付费镜像且使用了该共享镜像，则收取镜像费用。</td>
</tr>
</table>

