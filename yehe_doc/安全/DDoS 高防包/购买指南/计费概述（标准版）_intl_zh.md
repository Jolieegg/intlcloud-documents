﻿
## 标准版
腾讯云 DDoS 高防包（标准版）计费调整，新版计费规则已于**2022年03月24日**正式启用。

### 计费方式
 DDoS 高防包（标准版）承诺提供全力防护能力。全力防护指以成功防护每一次 DDoS 攻击为目标，整合当前本地清洗中心能力，全力对攻击进行抵御，同时随着腾讯云网络能力的不断提升，全力防护也会随之提升，无需您付出额外的升级成本。

>!如果您的业务遭受的 DDoS 攻击影响到腾讯云高防清洗中心的基础设施，则腾讯云保留压制流量的权利。 DDoS 高防包（标准版）实例受到流量压制时，可能对您的业务造成一定影响，例如业务访问流量可能会被限速，甚至被封堵。

 DDoS 高防包（标准版）有不同业务规模和防护 IP 数，并且仅支持按年开通服务（订购时长包括1年、2年、3年）。在选购时，单个实例的单价由您选择与自身业务规模匹配的实例规格决定。目前支持防护的地域：北京、上海、广州。

<table>
<thead>
<tr>
<th width="10%">计费参数</th>
<th width="10%">计费模式</th>
<th width="10%">付费方式</th>
<th width="70%">付费说明</th>
</tr>
</thead>
<tbody><tr>
<td>防护 IP 数</td>
<td>包年包月</td>
<td>预付费</td>
<td>选择需要使用  DDoS 高防包（标准版）实例防护的所有业务 IP 的数量，默认是10个，可选规格：10个、50个、100个。 若升级防护 IP 数，则在原有的基础上加收额外费用，仅可升不可降。</td>
</tr>
<tr>
<td rowspan=2>业务规模</td>
<td rowspan=2>包年包月</td>
<td>预付费</td>
<td>业务规模指被防护业务的正常业务规模，以带宽来衡量，入方向或出方向流量按每月最大值95消峰，单价请参见 <a href="https://www.tencentcloud.com/document/product/1029/55300#yw">业务规模价格说明</a>。  允许业务规模短期峰值超过购买的业务规模规格，但是如果一个月累计36小时超过规格，则全力防护会失效，仅保留原生防护的基础防护能力，正常业务带宽不会受到限制。</td>
</tr>
<tr> 
<td>后付费</td>
<td>开启弹性业务带宽后，超出预设定规格部分将按照超量部分收费，请合理评估业务带宽规模后选择规格。</td>
</tr>
</tbody></table>

>?
>- 需要选择与 CVM、CLB 等云资源相同地域的 DDoS 高防包（标准版），业务 IP 绑定后才实际生效。
>- 流量每月最大值95消峰： 以5分钟粒度进行采样，1个自然月为统计时长。月底将所有的采样点按峰值从高到低排序，去掉5%的最高峰值采样点，以第95%个最高峰作为95计费点带宽。

#### 弹性业务规模计算公式
弹性业务规模费用 =（本月95消峰后的最大业务规模 - 选定预付费的业务规模）* 业务规模单价。

### 产品价格

DDoS 高防包（标准版）默认支持保护单个地域下的业务 IP，防护 IP 数支持扩展。如果您需要保护多个地域下的 IP，则需要开通多个实例，若线上售卖的规格不满足您的业务需求，可以 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们定制。
>? 包年折扣与其他折扣不能同时享受，购买页面会自动选择较低折扣。

#### 业务规模价格说明[](id:yw)
<table>
<thead>
<tr>
<th  width="20%" rowspan=2>业务规模</th>
<th colspan=2>单价（预付费和后付费）</th>
</tr>
<tr>
<th>月刊例价</td>
<th>年刊例价</td>
</tr>
</thead>
<tbody>
<tr>
<td>0-1Gbps（含）</td>
<td>14美元/Mbps/月</td>
<td>160美元/Mbps/年</td>
</tr>
<tr>
<td>1-3Gbps（含）</td>
<td>10美元/Mbps/月</td>
<td>120美元/Mbps/年</td>
</tr>
<tr>
<td>3-10Gbps（含）</td>
<td>7美元/Mbps/月</td>
<td>80美元/Mbps/年</td>
</tr>
<tr>
<td>10Gbps以上</td>
<td>4美元/Mbps/月</td>
<td>40美元/Mbps/年</td>
</tr>
</tbody></table>

#### 防护 IP 数价格说明	
<table>
<thead>
<tr>
<th  width="20%" and rowspan=2>防护 IP 数</th>
<th  width="80%" and  colspan=1 >包月单价（单位：美元）</th>
</tr>
<tr>
<th>刊例价</th>
</tr>
</thead>
<tbody>
<tr>
<td>防护10个 IP</td>
<td>8890</td>
</tr>
<tr>
<td>防护50个 IP</td>
<td>17780</td>
</tr>
<tr>
<td>防护100个 IP</td>
<td>33333.33</td>
</tr>
</tbody></table>

<dx-alert infotype="explain" title="">
- 购买10IP 高防包默认赠送50 Mbps 业务规模。
- 购买50IP 高防包默认赠送300 Mbps 业务规模。
- 购买100IP 高防包默认赠送1000 Mbps 业务规模。
</dx-alert>

#### [CC 防护峰值说明](id:txfh)

<table>
<thead>
<tr>
<th width="20%">地区</th>
<th width="80%">CC 防护峰值</th>
</tr>
</thead>
<tbody><tr>
<td>广州</td>
<td>300,000QPS</td>
</tr>
<tr>
<td>上海</td>
<td>700,000QPS</td>
</tr>
<tr>
<td>北京</td>
<td>300,000QPS</td>
</tr>
</tbody></table>
