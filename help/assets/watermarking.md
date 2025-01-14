---
title: 向数字资产添加水印
description: 了解如何使用水印功能向资源添加数字水印。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
hide: true
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 3%

---

# 为您的数字资产添加水印 {#watermarking}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets] 允许您将数字水印添加到资产，以帮助用户验证资产的真实性和版权所有权。 [!DNL Experience Manager Assets] 支持在PNG和JPEG文件上用作水印的文本。

要对资产应用水印，请在中添加水印步骤 [!UICONTROL DAM更新资产] 工作流。

1. 访问 [!DNL Experience Manager] 用户界面，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 从 **[!UICONTROL 工作流模型]** 页面上，选择 **[!UICONTROL DAM更新资产]** 工作流并单击 **[!UICONTROL 编辑]**.

1. 从侧面板中，拖动 **[!UICONTROL 添加水印]** 逐步执行 [!UICONTROL DAM更新资产] 工作流。

   ![拖动 [!UICONTROL 添加水印] 步骤并将添加到 [!UICONTROL DAM更新资产] 工作流](assets/add_watermark_step_aem_assets.png)

   *图：拖动 [!UICONTROL 添加水印] 步骤并将添加到 [!UICONTROL DAM更新资产] 工作流。*

   >[!NOTE]
   >
   >放置 [!UICONTROL 添加水印] 在此之前的任何位置 [!UICONTROL 进程缩略图] 步骤。

1. 打开 **[!UICONTROL 添加水印]** 步骤以显示其属性。
1. 在 **[!UICONTROL 参数]** 制表符后，在各个字段中指定有效值，包括文本、字体类型、大小、颜色、位置、方向等。 要确认更改，请单击 **[!UICONTROL 完成]**.

   ![在中添加水印步骤中提供参数 [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *图：在添加水印步骤中提供参数 [!DNL Assets].*

1. 保存 **[!UICONTROL DAM更新资产]** 包含水印步骤的工作流。
1. 从 [!DNL Assets] 用户界面，上传示例资源。 水印以字体大小、颜色等显示在您在上述步骤中配置的位置。

要以编程方式或使用动态信息为PDF文档添加水印，请考虑使用 [Experience Manager文档服务](/help/forms/using/overview-aem-document-services.md) 主动出击。

## 提示和限制 {#tips-limitations}

* 仅支持基于文本的水印。 图像不会用作水印，即使您可以在创建 [!UICONTROL 添加水印进程].
* 仅支持PNG和JPEG文件添加水印。 其他资产格式没有添加水印。
