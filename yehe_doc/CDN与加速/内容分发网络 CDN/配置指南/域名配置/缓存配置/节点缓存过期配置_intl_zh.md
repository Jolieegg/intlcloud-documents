节点缓存过期配置可以设置源站资源在 CDN 节点的缓存过期时间，以调整源站资源在 CDN 节点缓存更新频率。您可以根据业务需求，按目录、文件后缀名、文件全路径配置资源的缓存过期时间。

## 功能介绍
CDN 会根据节点缓存过期配置的缓存过期时间，判断 CDN 节点的缓存资源是否过期。
- 若用户访问的资源在 CDN 节点的缓存未过期，CDN 节点直接将缓存返回给用户；
- 若用户访问的资源在 CDN 节点未缓存该资源或缓存已过期，则 CDN 节点会回源站获取最新资源并缓存到 CDN 节点，同时返回给用户。

若源站资源更新后，需要立刻更新 CDN 节点的缓存，可使用 [缓存刷新](https://console.cloud.tencent.com/cdn/refresh) 功能主动更新 CDN 节点未过期的缓存，使 CDN 节点缓存与源站资源保持一致。

## 注意事项
- 缓存过期时间会影响回源频率，建议根据实际业务需求设置资源缓存时长。缓存过期时间过短，会导致 CDN 频繁回源，增加源站的带宽；缓存过期时间过长，会导致 CDN 缓存更新慢，影响用户获取最新的资源。
- CDN 节点会按照 [腾讯云 CDN 缓存规则及优先级](#m1) 缓存资源。但 CDN 节点的缓存资源也可能因请求频率过低，在未达到缓存过期时间就提前从节点中删除。
- 建议您源站资源更新前后使用不同的名称，如以版本号（img-v1.jpg、img-v2.jpg）的方式命名内容不同的资源，避免源站变更资源的内容后，CDN 节点因缓存未过期仍使用旧的资源返回给用户。
- 若您仍使用旧版本（基础模式）的节点缓存过期配置，建议您按高级模式配置提交升级为最新版的节点缓存过期配置，以支持更多功能。需注意升级高级模式后不可恢复至原基础模式。旧版本的节点缓存过期配置文档查看：[节点缓存过期配置 (旧)](https://intl.cloud.tencent.com/document/product/228/35317)
- 源站可通过设置响应头 Cache-Control 控制 CDN 节点的缓存过期时间（缓存选项为：遵循源站），同时 CDN 节点将 Cache-Control 响应头传递给用户，实现控制浏览器的缓存时间。若需要由 CDN 节点设置浏览器的缓存时间，可通过 [浏览器缓存过期配置](https://intl.cloud.tencent.com/document/product/228/38932) 修改 CDN 节点响应给用户的 Cache-Control 头部。


## 配置说明
### 操作流程
1. 登录 [CDN 控制台](https://console.cloud.tencent.com/cdn)；
2. 单击左侧菜单内的**域名管理**，进入域名管理列表；
3. 选择需要配置的域名，单击**管理**进入域名配置页面；
4. 单击**缓存配置**，切换至缓存配置标签页，在标签页中，即可查看**节点缓存过期配置**；
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/cd08be49dbf25e88f28b32f019284231.png" width="850px">
<br>
5. 单击**新增规则**，可进入新增规则页面，新增节点缓存过期配置。
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/a57bc131850fc1a49c69e2aa86d0050e.png" width="450px">
<br>
<table>
<thead>
<tr>
<th>配置项</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td>类型</td>
<td>支持对全部文件、文件后缀、文件目录、全路径文件、首页进行配置：<br> 全部文件：指定全部文件设置规则，默认规则。<br> 文件后缀：指定文件的后缀设置规则。<br> 文件目录：指定文件的目录设置规则。<br> 全路径文件：指定文件的完整路径设置规则。<br> 首页：指定域名根目录设置规则。</td>
</tr>
<tr>
<td>内容</td>
<td>根据选择不同的文件类型，内容输入约束：</br>类型为全部文件时：固定为全部文件。</br>类型为文件后缀时：支持输入文件后缀名，多个以 “;” 为间隔。例如，jpg;png;css。</br>类型为文件目录时：支持输入文件目录，不能以 “/” 结尾，多个以 “;” 分隔。例如，/test;/a/b/c。</br>类型为全路径文件时：支持输入文件完整路径，多个以 “;” 分隔。例如，/index.html;/test/.jpg。</td>
</tr>
<tr>
<td>缓存选项</td>
<td>支持按照遵循源站、缓存、不缓存规则配置：<br> 遵循源站：按照源站响应头 Cache-Control 头部，设置 CDN 节点缓存时间，支持设置启发式缓存。 <br>缓存：自定义设置 CDN 节点的缓存时间，支持设置强制缓存。<br>不缓存：设置 CDN 节点 不缓存资源。<br></td>
</tr>
</tbody></table>

[](id:m1)	
### 腾讯云 CDN 缓存规则及优先级
#### 缓存选项为：遵循源站
<img src="https://qcloudimg.tencent-cloud.cn/raw/0d0086b11c0e9968707865af46a4c23d.jpg" width="850px">



CDN 节点将遵循源站响应头 Cache-Control 头部设置缓存时间。
- 源站响应头 Cache-Control 字段为 max-age，按照 max-age 值设置 CDN 节点缓存时间，如 Cache-Control：max-age=300，则缓存时间为 300 秒；
	- 源站响应头 Cache-Control 字段为 no-cache 或 no-store 或 private，CDN 节点不缓存资源；
	- 源站响应头没有 Cache-Control 或 Expires 时，按照启发式缓存状态设置缓存规则，详情如下：
		- 关闭启发式缓存，当源站响应头没有：Cache-Control 或 Expires 时，则缓存时间为 600 秒。
		- 开启启发式缓存，当源站响应头没有：Cache-Control 或 Expires 时，按照如下规则设置启发式缓存时间：
		 i. 默认配置：如果源站响应头存在 Last-Modified，则缓存时间=（当前时间 - Last-Modified）\* 0.1，如果源站响应头不存在 Last-Modified，则默认缓存时间为 600 秒。
		 <br>
		 <img src="https://qcloudimg.tencent-cloud.cn/raw/80612ba1e40f345e14b188939cb7b557.png" width="450px">
		 <br>
		 ii. <b>自定义策略</b>：可自定义设置启发式缓存的时间。
		 <br>
		 <img src="https://qcloudimg.tencent-cloud.cn/raw/06629eb849a9e56ee0c16db1f8bfe3c6.png" width="450px">
		 <br>

#### 缓存选项为：缓存
<img src="https://qcloudimg.tencent-cloud.cn/raw/dc781cff77d79f57fa3c9df800e21a4d.jpg" width="850px">

自定义设置 CDN 节点的缓存时间。	
- 关闭强制缓存：
	- 源站响应头 Cache-Control 字段为 max-age 或  源站响应头没有 Cache-Control ，按照自定义 CDN 节点缓存规则缓存。
	- 源站响应头 Cache-Control 字段为 no-cache 或 no-store 或 private，CDN 节点不缓存资源
	<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/35f0cf1d08f6395e541ec9c1c5ae364b.png" width="450px">
	<br>
- 开启强制缓存：忽略源站响应头Cache-Control ，按照自定义 CDN 节点缓存规则缓存。
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/fb2670449e6c40f5df4e8231c8f050b0.png" width="450px">
<br>

#### 缓存选项为：不缓存
设置 CDN 节点 不缓存资源。该资源的每个用户请求，CDN 节点都将直接回源获取资源响应给用户。
<img src="https://qcloudimg.tencent-cloud.cn/raw/621483c2535ca8e950e7a36c46c96983.png" width="450px">
<br>

#### 多条缓存规则优先级
若同时配置多条缓存规则时，底部规则**优先级大于**顶部规则。可通过单击**调整优先级**，拖动缓存规则顺序调整优先级。
<img src="https://qcloudimg.tencent-cloud.cn/raw/dcdbba45c63c0a18022fa73ecb76cb13.png" width="850px">	

### 推荐配置
- 不常更新的静态文件（例如，图片类型、应用下载类型等），建议设置30天。
- 频繁更新的静态文件（例如，js、css等），建议根据业务的更新频率设置缓存时间。
- 动态文件（例如，php、jsp、asp、aspx等动态文件），**需设置不缓存**。
- 其他涉及 **站点登入**（例如，wordpress 后台登入目录 /wp-admin）或 **接口查询** 等需要和源站直接交互的请求，**需设置不缓存**，否则可能导致访问错误。

	
### 配置约束
- 单个域名至多可添加100条缓存规则。
- 多条缓存规则优先级：底部优先级大于顶部。
- 单条文件后缀/文件目录/全路径文件规则中，至多可输入100组内容，不同内容之间用“;”分隔。例如：文件后缀  jpg;png。	
- 若您未配置任何规则或请求未命中配置的规则时，CDN 节点将遵循源站响应头 Cache-Control 头部设置缓存时间；若源站响应头没有 Cache-Control 字段，CDN 节点默认对该资源缓存600s。
- CDN 节点仅缓存 GET、HEAD 请求类型的请求内容，其余 POST、OPTIONS 等请求类型的请求内容，CDN 节点不缓存。


## 配置示例
### 示例1
原缓存规则为：php;jsp;asp;aspx文件后缀的资源不缓存，其余全部文件缓存30天。
<img src="https://qcloudimg.tencent-cloud.cn/raw/5129af6e01dd139afcf5c44a7ba97ef3.png" width="850px">
<br>
现需要增加：jpg、png文件后缀的资源缓存10天，且需要忽略源站响应头 Cache-Control ，即开启强制缓存；其余全部文件的缓存规则修改为遵循源站。

1. 单击**新增规则**，类型为文件后缀，内容为jpg;png，缓存选项为缓存，缓存时间为10天，强制缓存为是，单击**确定**。
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/a1db0f8cbc470efa0b5749114ca8ea07.png" width="450px">
<br>
2. 选择全部文件的缓存规则，单击**修改**，修改缓存选项为遵循源站，单击**确定**。
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/c0442f19e230b69456f59d1874d784a9.png" width="450px">
<br>
3. 调整完成后的缓存规则为：
	- jpg、png 文件后缀的资源缓存10天，强制缓存；
	- php;jsp;asp;aspx 文件后缀的资源不缓存；
	- 其余全部文件缓存30天。
	<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/bfc24f2fca1ab9a184b0bf415c85a0f4.png" width="850px">
	<br>
	则实际缓存情况如下：
	-  `www.test.com/abc.jpg`  资源节点缓存时间为10天，即使源站响应头 Cache-Control 字段为 no-cache 或 no-store 或 private。
	-  `www.test.com/def.php`  资源不会缓存至节点；

	
### 示例2
**使用 WordPress 建站的节点缓存过期配置建议：**
- 后台登入地址/wp-admin目录下的资源，需要设置不缓存，否则会导致后台登入相关资源被缓存，登录出错。如果有其他接口相关的资源，同样需要设置不缓存。
- php;jsp;asp;aspx 动态文件后缀的资源，需要设置不缓存（CDN 默认缓存规则）；
- html;js;css 后缀文件更新较频繁，需要根据更新频率设置缓存时间。建议设置缓存时间7天，不设置强制缓存；
- 其余全部文件缓存30天（CDN 默认缓存规则）。

**在 CDN 默认缓存规则的基础下，按如下操作新增规则：**
1. 单击**新增规则**，类型为目录，内容为 /wp-admin，缓存选项为不缓存，单击**确定**。
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/93a9e55ac5c35bbe1e955eda302f41f1.png" width="450px">
<br>
2. 单击**新增规则**，类型为文件后缀，内容为 html;js;css，缓存选项为缓存，缓存时间为7天，强制缓存为否，单击**确定**。
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/1e0248cf175dd0158f73300d3bf7dc2f.png" width="450px">
<br>
3. 按照优先级顺序，底部优先级高于顶部，单击**调整优先级**，拖动"/wp-admin目录不缓存规则"规则调整至底部，使该规则优先级最高。
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/ba9b0809fc20a354ebadfbed4f19eee5.png" width="850px">
<br>
4.调整完成后的缓存规则为：
	- /wp-admin 目录下的所有资源不缓存；
	- html;js;css 文件后缀的资源缓存7天；
	- php;jsp;asp;aspx 文件后缀的资源不缓存；
	- 其余全部文件缓存30天。
	<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/da6e9921da144c97f7b80e569f2d8444.png" width="850px">
<br>

## 常见问题
- [源站变更文件后，CDN 加速节点上的缓存会主动、实时更新的吗？](https://intl.cloud.tencent.com/document/product/228/11203)
- [如何判断用户访问是否命中 CDN 节点缓存？](https://intl.cloud.tencent.com/document/product/228/11203)
