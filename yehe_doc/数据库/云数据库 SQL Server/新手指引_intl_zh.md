﻿本文介绍云数据库 SQL Server 产品的使用过程中的常用场景及相关操作，为刚入门云数据库 SQL Server 的用户提供一条学习的路径。

## 1. 熟悉云数据库 SQL Server 的基础知识
如果您是首次购买及使用云数据库 SQL Server，建议您按照以下顺序先了解产品的相关介绍和概念。
- [产品概述](https://intl.cloud.tencent.com/document/product/238/2016)
- [产品架构](https://intl.cloud.tencent.com/document/product/238/3254)
- [产品优势](https://intl.cloud.tencent.com/document/product/238/6985)
- [应用场景](https://intl.cloud.tencent.com/document/product/238/3248)
- [常用概念](https://intl.cloud.tencent.com/document/product/238/46489)
- [地域和可用区](https://intl.cloud.tencent.com/document/product/238/7520)
- [功能概览及差异](https://intl.cloud.tencent.com/document/product/238/46495)
- [实例类型](https://intl.cloud.tencent.com/document/product/238/46494)
- [主实例规格](https://intl.cloud.tencent.com/document/product/238/46492)
- [只读实例规格](https://intl.cloud.tencent.com/document/product/238/46493)
- [存储类型](https://intl.cloud.tencent.com/document/product/238/46490)
- [网络环境](https://intl.cloud.tencent.com/document/product/238/32562)
- [许可声明](https://intl.cloud.tencent.com/document/product/238/6986)

了解产品相关介绍和概念之后，我们给出了在使用云数据库 SQL Server 时需要了解的产品使用限制以及使用规范建议，帮助您规范使用本产品。
- [约束与限制](https://intl.cloud.tencent.com/document/product/238/2021)
- [使用规范与建议](https://intl.cloud.tencent.com/document/product/238/48122)

## 2. 云数据库 SQL Server 的计费模式
云数据库 SQL Server 的计费模式为按量计费。您需要全面了解云数据库 SQL Server 的计费模式，有利于您选择最优的计费方案。详情请参见 [计费概述](https://intl.cloud.tencent.com/document/product/238/35798)。
更多与产品计费相关的介绍及说明，您还可以了解以下文章。

- [主实例价格](https://www.tencentcloud.com/document/product/238/55087)
- [只读实例价格](https://www.tencentcloud.com/document/product/238/53999)
- [续费说明](https://www.tencentcloud.com/document/product/238/3116)
- [欠费说明](https://intl.cloud.tencent.com/document/product/238/3117)
- [退费说明](https://intl.cloud.tencent.com/document/product/238/31431)
- [调整实例费用说明](https://intl.cloud.tencent.com/document/product/238/35799)
- [本地备份空间收费说明](https://intl.cloud.tencent.com/document/product/238/45849)
- [跨地域备份收费说明](https://intl.cloud.tencent.com/document/product/238/50229)
- [查看账单明细](https://intl.cloud.tencent.com/document/product/238/47424)

## 3. 新手入门
### 3.1  购买 SQL Server 实例
在使用云数据库 SQL Server 之前，您需要注册腾讯云账号并且购买云数据库 SQL Server 服务。详情请参见 [购买 SQL Server 实例](https://intl.cloud.tencent.com/document/product/238/31571)。
### 3.2 连接 SQL Server 实例
购买实例后，您可通过 Windows 云服务器或 Linux 云服务器，以内外网两种不同的方式访问云数据库 SQL Server。详情请参见 [连接 SQL Server 实例](https://intl.cloud.tencent.com/document/product/238/48065)。
### 3.3 管理 SQL Server 实例
在创建完云数据库 SQL Server 实例之后，您可通过控制台对 SQL Server 实例进行管理操作，详细请参见 [管理 SQL Server 实例](https://intl.cloud.tencent.com/document/product/238/35800)。

## 4. 控制台功能概述
云数据库 SQL Server 为您提供可便捷操作的控制台，帮助您实现轻松管理实例、一键升降配、可视化监控实例、设置管理备份等丰富多样化的功能，对应的操作文档如下表所示。

<table>
<thead><tr><th>控制台功能</th><th>操作文档</th></tr></thead>
<tbody><tr>
<td>维护管理实例</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/46508" target="_blank">修改实例名称</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46507" target="_blank">设置实例备注</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46506" target="_blank">设置实例标签</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35786" target="_blank">设置实例所属项目</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/50258" target="_blank">修改实例级字符集规则</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/50257" target="_blank">修改系统时区</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35785" target="_blank">设置实例维护信息</a></li><li><a href="https://www.tencentcloud.com/document/product/238/50256" target="_blank">多可用区容灾</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46505" target="_blank">重启实例</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35787" target="_blank">销毁实例</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/42695" target="_blank">跨可用区迁移</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46504" target="_blank">回收站</a></li></ul></td></tr>
<tr>
<td>调整实例配置</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/44352" target="_blank">调整实例配置概述</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/44353" target="_blank">调整实例架构</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/44354" target="_blank">调整实例版本</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35783" target="_blank">调整实例规格</a></li></ul></td>
</tr>
<tr>
<td>只读实例</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/43142" target="_blank">只读实例概述</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/43143" target="_blank">管理只读实例</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/43144" target="_blank">只读实例 RO 组</a></li></ul></td></tr>
<tr>
<td>网络与安全</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/46498" target="_blank">基础网络转 VPC 网络</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46497" target="_blank">更改网络（VPC 转 VPC）</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/50230" target="_blank">开启或关闭外网地址</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/48066" target="_blank">通过 CLB 开启外网服务</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35789" target="_blank">配置安全组</a></li>访问管理<li><a href="https://intl.cloud.tencent.com/document/product/238/34583" target="_blank">访问管理概述</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/34584" target="_blank">授权策略语法</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/34585" target="_blank">可授权的资源类型</a></li></ul></td>
</tr>
<tr>
<td>账号管理</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/7521" target="_blank">创建账号</a></li><li><a href="https://www.tencentcloud.com/document/product/238/54446" target="_blank">创建超级权限账号</a></li><li><a href="https://www.tencentcloud.com/document/product/238/54445" target="_blank">创建特殊权限账号</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35796" target="_blank">重置密码</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35795" target="_blank">修改账号权限</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35794" target="_blank">删除账号</a></li></ul></td>
</tr>
<tr>
<td>数据库管理</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/35780" target="_blank">创建数据库</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/47425" target="_blank">设置数据库权限</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/47426" target="_blank">克隆数据库</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35781" target="_blank">删除数据库</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/41608" target="_blank">变更数据捕获 CDC</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/41607" target="_blank">更改跟踪 CT</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/41606" target="_blank">收缩数据库</a></li></ul></td>
</tr>
<tr>
<td>参数配置</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/41609" target="_blank">设置实例参数</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/41610" target="_blank">查看参数修改历史</a></li></ul></td>
</tr>
<tr>
<td>监控与告警</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/46503" target="_blank">查看监控图表</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46502" target="_blank">支持的监控指标</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46501" target="_blank">设置告警策略</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46500" target="_blank">设置告警通知</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46499" target="_blank">查看告警历史</a></li></ul></td>
</tr>
<tr>
<td>备份与回档</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/45857" target="_blank">备份概述</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/45855" target="_blank">设置自动备份</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/45854" target="_blank">创建手动备份</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/45853" target="_blank">配置备份任务</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/49138" target="_blank">跨地域备份</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/45852" target="_blank">查看备份列表</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/7523" target="_blank">下载备份</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/45851" target="_blank">删除手动备份</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/45850" target="_blank">查看备份空间</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/7522" target="_blank">回档方案概览</a></li><li><a href="https://www.tencentcloud.com/document/product/238/55305" target="_blank">回档至当前实例</a></li><li><a href="https://www.tencentcloud.com/document/product/238/55306" target="_blank">回档至已有实例（同地域）</a></li><li><a href="https://www.tencentcloud.com/document/product/238/55307" target="_blank">回档至已有实例（跨地域）</a></li></ul></td>
</tr>
<tr>
<td>日志管理</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/47569" target="_blank">查询和下载慢查询日志</a></li><li>查询和下载阻塞事件及死锁事件</li></ul></td>
</tr>
<tr>
<td>发布订阅</td>
<td><ul><li>发布订阅概述</li><li>管理发布订阅</li></ul></td>
</tr>
<tr>
<td>数据集成服务（SSIS）</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/75223" target="_blank">数据集成服务（SSIS）概述</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/75224" target="_blank">购买商业智能服务器</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/75225" target="_blank">创建 Windows 鉴权账号</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/75226" target="_blank">添加平面文件</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/75227" target="_blank">互通源目标实例及商业智能服务器</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/75228" target="_blank">部署项目</a></li></ul></td>
</tr>
<tr>
<td>数据迁移（新版）</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/39005" target="_blank">冷备迁移</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/39006" target="_blank">使用 DTS 迁移数据</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/39006#.E8.BF.81.E7.A7.BB.E5.89.8D.E6.A0.A1.E9.AA.8C.E5.A4.B1.E8.B4.A5.E9.94.99.E8.AF.AF.E8.AF.A6.E6.83.85.E5.8F.8A.E8.A7.A3.E5.86.B3.E6.96.B9.E6.A1.88" target="_blank">迁移前校验失败错误详情及解决方案</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/39006#.E8.BF.81.E7.A7.BB.E4.B8.AD.E4.BB.BB.E5.8A.A1.E5.A4.B1.E8.B4.A5.E9.94.99.E8.AF.AF.E8.AF.A6.E6.83.85.E5.8F.8A.E8.A7.A3.E5.86.B3.E6.96.B9.E6.A1.88" target="_blank">迁移中任务失败错误详情及解决方案</a></li><li><a href="https://www.tencentcloud.com/document/product/238/53570" target="_blank">使用 DTS 跨账号迁移数据</a></li></ul></td>
</tr>
</tbody></table>


## 5. 新手常见问题
我们为您总结了在使用云数据库 SQL Server 中的常见问题，方便您查询和获取解决常见问题的方法。详细请参见 [常见问题概览](https://intl.cloud.tencent.com/document/product/238/47719)。

## 6. 常见故障处理
当您在使用云数据库 SQL Server 出现 CPU 使用率高、阻塞问题、慢 SQL、死锁跟踪等问题时，可参见 [常见问题故障处理](https://intl.cloud.tencent.com/document/product/238/47626) 了解对应问题情况和排查处理方法。

## 7. 反馈与建议
使用云数据库 SQL Server 产品和服务中有任何问题或建议，您可以通过以下渠道反馈，将有专人跟进解决您的问题：
- 如果发现产品文档的问题，如链接、内容、API 错误等，您可以单击文档页右侧**文档反馈**或选中存在问题的内容进行反馈。
- 如果遇到产品相关问题，您可咨询 [在线支持](https://cloud.tencent.com/online-service) 寻求帮助。
- 如果您有其他疑问，可前往 [腾讯云开发者社区](https://cloud.tencent.com/developer/tag/105?entry=ask) 进行提问。
