---
title: 将Landing Pages与Adobe Analytics集成
description: 了解如何将登陆页面与Adobe Analytics集成。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 将Landing Pages与Adobe Analytics集成{#integrating-landing-pages-with-adobe-analytics}

AEM已将登陆页面解决方案与集成 [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) 通过以下行动号召(CTA)组件：

1. 点进组件
1. 图形链接组件

这些组件展示某些可通过Adobe Analytics变量（流量、转化变量）和成功事件映射的属性，以将信息发送到Adobe Analytics。

## 前提条件 {#prerequisites}

Adobe建议您浏览 [现有AEM-Adobe Analytics集成](/help/sites-administering/adobeanalytics.md) 以了解此集成的工作方式。

## 可用于映射的组件 {#components-available-for-mapping}

在AEM中， **行动动员** 组件 —  **点进链接** 和 **GraphicalLink**  — 显示在sidekick的此处，可以映射到Adobe Analytics变量。

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### 将登陆页面组件映射到Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

要将登陆页面组件映射到Adobe Analytics，请执行以下操作：

1. 在创建Adobe Analytics配置并创建框架后，从下拉菜单中选择相应的报表包。 这会导致提取Adobe Analytics变量并在内容查找器中显示它们。
1. 根据需要，将行动号召(CTA)组件从Sidekick拖放到页面中部的映射区域。

<table>
 <tbody>
  <tr>
   <td><strong>组件名称</strong></td>
   <td><strong>公开的属性</strong></td>
   <td><strong>属性的含义</strong></td>
  </tr>
  <tr>
   <td><strong>CTA点进链接</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>链接上的标签或链接的文本 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>事件数据.clickthroughLinkTarget</i> <br /> </td>
   <td>单击链接时拍摄的目标 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>点击事件 </td>
  </tr>
  <tr>
   <td><strong>CTA图形链接</strong></td>
   <td><i>eventdata.clickthroughImageLabel</i> <br /> </td>
   <td>CTA图像的标题 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageTarget</i> <br /> </td>
   <td>单击包含链接的图像时拍摄的目标</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickgroughImageAsset</i> <br /> </td>
   <td>存储库中图像资源的路径 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughImageClick</i> <br /> </td>
   <td>点击事件</td>
  </tr>
 </tbody>
</table>

1. 将这些公开的属性与内容查找器中的任何Adobe Analytics变量进行映射。 该框架现在可以使用。
1. 您现在可以创建登陆页面，或使用现有CTA组件打开现有登陆页面，然后单击 **Cloud Service** tab in **页面属性** 从sidekick(在触屏优化UI中，选择 **打开属性** 并单击 **Cloud Service**)并配置要与登陆页面一起使用的框架。 从下拉列表中选择框架。

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 使用登陆页配置框架后，您现在可以使用检测出的组件，并且CTA上的任何点击都记录在Adobe Analytics中。
