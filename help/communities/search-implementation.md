---
title: Search Essentials
description: 了解搜索功能，该功能是AEM Communities的一项基本功能。 社区还为用户生成的内容提供搜索API。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 4%

---

# Search Essentials {#search-essentials}

## 概述 {#overview}

搜索功能是Adobe Experience Manager (AEM)社区的一项基本功能。 除了 [AEM平台搜索](../../help/sites-deploying/queries-and-indexing.md) 功能，AEM Communities提供了 [UGC搜索API](#ugc-search-api) 用于搜索用户生成的内容(UGC)。 UGC具有独特的属性，因为它与其他AEM内容和用户数据分开输入和存储。

对于Communities，通常搜索的两项内容是：

* 社区成员发布的内容

   * 它使用AEM Communities的UGC搜索API。

* 用户和用户组（用户数据）

   * 它使用AEM平台搜索功能。

文档中的此部分与创建自定义组件（用于创建或管理UGC）的开发人员有关。

## 安全和影子节点 {#security-and-shadow-nodes}

对于自定义组件，必须使用 [SocialResourceUtities](socialutils.md#socialresourceutilities-package) 方法。 创建和搜索UGC的实用程序方法建立了所需的 [影子节点](srp.md#about-shadow-nodes-in-jcr) 并确保成员拥有请求的正确权限。

不通过SRP实用程序管理的是与审核相关的属性。

请参阅 [SRP和UGC Essentials](srp-and-ugc.md) 有关用于访问UGC和ACL影子节点的实用程序方法的信息。

## UGC搜索API {#ugc-search-api}

此 [UGC公用存储](working-with-srp.md) 由各种存储资源提供者(SRP)之一提供，每个提供者可能具有不同的本地查询语言。 因此，无论选择哪个SRP，自定义代码都应使用来自 [UGC API包](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*)调用适用于所选SRP的查询语言。

### ASRP搜索 {#asrp-searches}

对象 [ASRP](asrp.md)，UGC存储在Adobe云中。 虽然UGC在CRX中不可见， [审核](moderate-ugc.md) 在创作环境和发布环境中均可用。 对的使用 [UGC搜索API](#ugc-search-api) 适用于ASRP的方式与其他SRP相同。

当前不存在用于管理ASRP搜索的工具。

在创建可搜索的自定义属性时，必须遵守 [命名要求](#naming-of-custom-properties).

### MSRP搜索 {#msrp-searches}

对象 [MSRP](msrp.md)，UGC存储在配置为使用Solr进行搜索的MongoDB中。 UGC在CRX中不可见，但是 [审核](moderate-ugc.md) 在创作环境和发布环境中均可用。

关于MSRP和Solr：

* AEM平台的嵌入式Solr不用于MSRP。
* 如果对AEM平台使用远程Solr，则可以与MSRP共享，但它们应使用不同的集合。
* Solr可以配置为标准搜索或多语言搜索(MLS)。
* 有关配置详细信息，请参阅 [Solr配置](msrp.md#solr-configuration) 用于MSRP。

自定义搜索功能应使用 [UGC搜索API](#ugc-search-api).

在创建可搜索的自定义属性时，必须遵守 [命名要求](#naming-of-custom-properties).

### JSRP搜索 {#jsrp-searches}

对象 [JSRP](jsrp.md)，UGC存储在 [Oak](../../help/sites-deploying/platform.md) 并且仅在输入它的AEM Author或Publish实例的存储库中可见。

由于UGC通常输入在发布环境中，因此对于多发布者生产系统，有必要配置 [发布集群](topologies.md)，而不是发布场，因此输入的内容对所有发布者可见。

对于JSRP，在发布环境中输入的UGC在创作环境中从不可见。 因此，所有 [审核](moderate-ugc.md) 任务在“发布”环境中执行。

自定义搜索功能应使用 [UGC搜索API](#ugc-search-api).

#### Oak索引 {#oak-indexing}

虽然从AEM 6.2开始，AEM平台搜索不会自动创建Oak索引，但已为AEM Communities添加这些索引，以改进性能并在显示UGC搜索结果时支持分页。

如果自定义属性正在使用中并且搜索缓慢，则必须为自定义属性创建其他索引以提高其性能。 要保持可移植性，请遵守 [命名要求](#naming-of-custom-properties) 创建可搜索的自定义属性时。

要修改现有索引或创建自定义索引，请参见 [Oak查询和索引](../../help/sites-deploying/queries-and-indexing.md).

此 [Oak索引管理器](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) 可从ACS AEM Commons获取。 它提供：

* 现有索引的视图。
* 启动重新索引的功能。

查看现有Oak索引的方式 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)，位置为：

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## 索引搜索属性 {#indexed-search-properties}

### 默认搜索属性 {#default-search-properties}

以下是用于各种Communities功能的一些可搜索属性：

| **属性** | **数据类型** |
|---|---|
| isFlagged | *布尔型* |
| isSpam | *布尔型* |
| 读取 | *布尔型* |
| 影响 | *布尔型* |
| 附件 | *布尔型* |
| 情绪 | *长整型* |
| 已标记 | *布尔型* |
| 已添加 | *日期* |
| modifieddate | *日期* |
| 状态 | *字符串* |
| 用户标识符 | *字符串* |
| 回复 | *长整型* |
| jcr:title | *字符串* |
| jcr：description | *字符串* |
| sling:resourceType | *字符串* |
| allowThreadedReply | *布尔型* |
| isDraft | *布尔型* |
| publishdate | *日期* |
| publishJobId | *字符串* |
| 已回复 | *布尔型* |
| chosenanswered | *布尔型* |
| 标记 | *字符串* |
| cq：Tag | *字符串* |
| author_display_name | *字符串* |
| location_t | *字符串* |
| 父路径 | *字符串* |
| parentTitle | *字符串* |

### 自定义属性的命名 {#naming-of-custom-properties}

添加自定义属性时，要使这些属性对使用创建的排序和搜索可见 [UGC搜索API](#ugc-search-api)，它是 *必填* 以向属性名称添加后缀。

后缀用于使用架构的查询语言：

* 它将该属性标识为可搜索。
* 它标识数据类型。

Solr是使用架构的查询语言的示例。

| **后缀** | **数据类型** |
|---|---|
| _b | *布尔型* |
| _dt | *日程表* |
| _d | *双精度型* |
| _tl | *长整型* |
| _s | *字符串* |
| _t | *文本* |

**注释:**

* *文本* 是一个标记化字符串， *字符串* 不是。 使用 *文本* 用于模糊（更类似于）搜索。

* 对于多值类型，请将“s”添加到后缀，例如：

   * `viewDate_dt`：单一日期属性
   * `viewDates_dts`：日期列表属性

## 过滤器 {#filters}

组件，包括 [评论系统](essentials-comments.md)中，除了其端点外，还支持过滤器参数。

AND和OR逻辑的过滤器语法如下所示（在URL编码之前显示）：

* 要指定OR或使用带有逗号分隔值的过滤器参数，请执行以下操作：

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* 要指定AND使用多个过滤器参数，请执行以下操作：

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

的默认实施 [搜索组件](search.md) 使用此语法，就像在打开搜索结果页面的URL [社区组件指南](components-guide.md). 要试验，请浏览 [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

筛选器运算符为：

| EQ | equals |
|---|---|
| NE | 不等于 |
| LT | 小于 |
| LTE | 小于或等于 |
| 通用电气 | 大于 |
| GTE | 大于或等于 |
| 点赞 | 模糊匹配 |

URL引用Communities组件（资源），而不是引用放置该组件的页面，这一点很重要：

* 正确：论坛组件
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* 不正确：论坛页面
   * `/content/community-components/en/forum.social.json`

## SRP工具 {#srp-tools}

有一个Adobe Experience Cloud GitHub项目，该项目包含：

[AEM Communities SRP工具](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

此存储库包含用于管理SRP中数据的工具。

目前，有一个servlet可以从任何SRP中删除所有UGC。

例如，要删除ASRP中的所有UGC，请执行以下操作：

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## 疑难解答 {#troubleshooting}

### Solr查询 {#solr-query}

要帮助解决Solr查询的问题，请为以下对象启用DEBUG日志记录

`com.adobe.cq.social.srp.impl.SocialSolrConnector`。

实际Solr查询在调试日志中显示编码的URL：

要查询的solr为： `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

的值 `q` 参数为查询。 解码URL编码后，可将查询传递到Solr管理员查询工具进行进一步调试。

## 相关资源 {#related-resources}

* [社区内容存储](working-with-srp.md)  — 讨论UGC公用存储的可用SRP选项。
* [存储资源提供程序概述](srp.md)  — 简介和存储库使用情况概述。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。
* [SocialUtils重构](socialutils.md)  — 用于替换SocialUtils的SRP的实用程序方法。
* [搜索和搜索结果组件](search.md)  — 将UGC搜索功能添加到模板。
