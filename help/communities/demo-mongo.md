---
title: 如何设置MongoDB以进行演示
description: 如何为一个创作实例和一个发布实例设置MSRP
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# 如何设置MongoDB以进行演示 {#how-to-setup-mongodb-for-demo}

## 简介 {#introduction}

本教程将介绍如何设置 [MSRP](msrp.md) 对象 *一位作者* 实例和 *一个发布* 实例。

通过此设置，可从创作和发布环境访问社区内容，而无需转发或反向复制用户生成的内容(UGC)。

此配置适用于 *非生产* 环境，例如用于开发和/或演示。

**A *生产* 环境应：**

* 使用副本集运行MongoDB
* 使用SolrCloud
* 包含多个发布服务器实例

## MongoDB {#mongodb}

### 安装MongoDB {#install-mongodb}

* 下载MongoDB，从 [https://www.mongodb.com/](https://www.mongodb.com/)

   * 操作系统选择：

      * Linux®
      * Mac 10.8
      * Windows 7

   * 版本选择：

      * 至少应使用版本2.6

* 基本配置

   * 按照MongoDB安装说明操作。
   * 为mongod配置：

      * 无需配置蒙兀国或分片。

   * 已安装的MongoDB文件夹名为 &lt;mongo-install>.
   * 所定义的数据目录路径称为 &lt;mongo-dbpath>.

* MongoDB可以与AEM在同一主机上运行或远程运行。

### 启动MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath &lt;mongo-dbpath>

这会使用默认端口27017启动MongoDB服务器。

* 对于Mac，使用起始引号“ulimit -n 2048”增加ulimit

>[!NOTE]
>
>如果MongoDB已启动 *之后* AEM， **重新启动** 所有 **AEM** 实例以使其正确连接到MongoDB。

### 演示生产选项：设置MongoDB副本集 {#demo-production-option-setup-mongodb-replica-set}

以下命令是使用3个节点在localhost上设置复制副本集的示例：

* `bin/mongod --port 27017 --dbpath data --replSet rs0&`
* `bin/mongo`

   * `cfg = {"_id": "rs0","version": 1,"members": [{"_id": 0,"host": "127.0.0.1:27017"}]}`
   * `rs.initiate(cfg)`

* `bin/mongod --port 27018 --dbpath data1 --replSet rs0&`
* `bin/mongod --port 27019 --dbpath data2 --replSet rs0&`
* `bin/mongo`

   * `rs.add("127.0.0.1:27018")`
   * `rs.add("127.0.0.1:27019")`
   * `rs.status()`

## Solr {#solr}

### 安装Solr {#install-solr}

* 下载Solr，从 [Apache Lucene](https://archive.apache.org/dist/lucene/solr/)：

   * 适用于任何操作系统。
   * Solr版本7.0。
   * Solr需要Java™ 1.7或更高版本。

* 基本配置

   * 执行“example”Solr设置。
   * 无需服务。
   * 已安装的Solr文件夹称为 &lt;solr-install>.

### 为AEM Communities配置Solr {#configure-solr-for-aem-communities}

要为MSRP配置Solr收藏集以进行演示，需要做出两个决定（有关详细信息，请选择主文档的链接）：

1. 以独立方式运行Solr或 [SolrCloud模式](msrp.md#solrcloudmode).
1. 安装 [标准](msrp.md#installingstandardmls) 或 [高级](msrp.md#installingadvancedmls) 多语言搜索(MLS)。

### 独立Solr {#standalone-solr}

运行Solr的方法可能会因安装版本和方式而异。 此 [Solr参考指南](https://archive.apache.org/dist/lucene/solr/ref-guide/) 是权威文档。

为简单起见，使用版本4.10作为示例，在独立模式下启动Solr：

* cd到 &lt;solrinstall>/example
* Java™ -jar start.jar

此过程使用默认端口8983启动Solr HTTP服务器。 您可以浏览到Solr控制台以获取用于测试的Solr控制台。

* 默认Solr控制台： [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>如果Solr Console不可用，请检查下的日志 &lt;solrinstall>/example/logs. 查看SOLR是否尝试绑定到无法解析的特定主机名（例如“user-macbook-pro”）。
>
如果是这样，请更新 `etc/hosts` 文件，其中包含此主机名的新条目（例如，127.0.0.1 user-macbook-pro），以便正确启动Solr。

### SolrCloud {#solrcloud}

要运行基本（非生产）solrCloud安装程序，请通过以下方式启动solr：

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## 将MongoDB标识为公用存储 {#identify-mongodb-as-common-store}

如有必要，启动创作和发布AEM实例。

如果AEM在MongoDB启动之前正在运行，则必须重新启动AEM实例。

按照主文档页面上的说明进行操作： [MSRP - MongoDB公用存储](msrp.md)

## 测试 {#test}

要测试和验证MongoDB公用存储，请在发布实例上发布评论并在创作实例上查看该评论，然后在MongoDB和Solr中查看UGC：

1. 在发布实例上，浏览到 [社区组件指南](http://localhost:4503/content/community-components/en/comments.html) 页面并选择注释组件。
1. 登录以发布评论：
1. 在注释文本输入框中输入文本，然后单击 **[!UICONTROL Post]**

   ![post-comment](assets/post-comment.png)

1. 只需在 [创作实例](http://localhost:4502/content/community-components/en/comments.html) （可能仍以管理员/管理员身份登录）。

   ![view-comment](assets/view-comment.png)

   注意：尽管JCR节点位于 *asipath* 在作者中，这些节点用于SCF框架。 实际的UGC不在JCR中，而是在MongoDB中。

1. 在mongodb中查看UGC **[!UICONTROL Communities]** > **[!UICONTROL 收藏集]** > **[!UICONTROL 内容]**

   ![ugc-content](assets/ugc-content.png)

1. 在Solr中查看UGC：

   * 浏览到Solr功能板： [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * 用户 `core selector` 以选择 `collection1`.
   * 选择 `Query`.
   * 选择 `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## 疑难解答 {#troubleshooting}

### 未显示UGC {#no-ugc-appears}

1. 确保MongoDB已安装并正常运行。

1. 确保已将MSRP配置为默认提供程序：

   * 在所有创作和发布AEM实例上，重新访问 [存储配置控制台](srp-config.md)，或检查AEM存储库：

   * 在JCR中，如果 [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) 不包含 [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) 节点，这意味着存储提供程序是JSRP。
   * 如果srpc节点存在且包含节点 [默认配置](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，默认配置的属性应将MSRP定义为默认提供程序。

1. 确保选择MSRP后重新启动AEM。
