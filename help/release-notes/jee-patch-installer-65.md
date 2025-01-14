---
title: AEM Forms JEE修补程序安装程序
description: 了解如何使用AEM Forms JEE修补程序安装程序来修复AEM 6.5 Forms组件中的问题。
content-type: reference
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: 6b24067c1808475044a612f21d5d4d2793c13e17
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 18%

---

# AEM Forms JEE修补程序安装程序 {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[联系支持人员](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support) 以获取详细信息或获取修补程序。

## 关于修补程序安装程序 {#about-the-patch-installer}

AEM 6.5 Forms JEE修补程序安装程序包含在此修补程序发布之前可用的AEM 6.5 Forms JEE所有组件的所有已修复问题。 查看最新信息  [Service Pack发行说明](release-notes.md) 以获取已修复问题的完整列表。

## 安装补丁程序的先决条件 {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## 安装和配置修补程序 {#installing-and-configuring-the-patch}

1. 备份&lt;*AEM_forms_root*>/部署文件夹。 如果您决定卸载快速修补程序，则必须执行此操作。
1. 停止应用程序服务器。
1. 将补丁安装程序存档文件提取到硬盘驱动器。
1. 在根据您所使用的操作系统命名的目录中：

   * **Windows**
导航到安装介质上的相应目录或硬盘上复制安装程序的文件夹，然后双击aemforms65_cfp_install.exe文件。

      * （Windows 32位） `Windows\Disk1\InstData\VM`
      * （Windows 64位） `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
导航到相应的目录，然后在命令提示符下键入 `./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   这会启动安装向导，引导您完成安装。

1. 在“Introduction”面板上，单击 **[!UICONTROL Next]**。
1. 在 **选择安装文件夹** 屏幕，验证显示的默认位置对于您的现有安装是否正确，或者单击 **[!UICONTROL 浏览]** 选择安装AEM表单的备用文件夹，然后单击 **[!UICONTROL 下一个]**.
1. 阅读“Quick Fix Patch Summary”信息，然后单击 **[!UICONTROL Next]**。
1. 阅读“Pre-Installation Summary”信息，然后单击 **[!UICONTROL Install]**。
1. 安装完成后，单击 **[!UICONTROL Next]** 以将快速修补程序更新应用到已安装的文件。

1. **[仅适用于Windows]：** 执行以下操作：
   * 取消选择 **启动Configuration Manager** 选项，然后再单击 **[!UICONTROL 完成]**. 运行 **配置管理器** 通过使用 **ConfigurationManager.bat** 文件位置 `[aem-forms root]\configurationManager\bin`.

   * 或者取消选择 **启动Configuration Manager** 选项，然后再单击 **[!UICONTROL 完成]**. 运行之前 **配置管理器** 使用 **Configurationmanager.exe** 或 **ConfigurationManager_IPv6.exe**，导航到 *`<AEMForms_Install_Dir>\configurationManager\bin`* 目录并替换 **配置管理器.lax** 和 **ConfigurationManager_IPV6.lax** 使用最新的 [配置管理器.lax](/help/assets/ConfigurationManager.lax) 和 [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) 文件、搜索和替换 **axis-1.4.1.1.jar** 替换为 **axis-1.4.1.2.jar** 在这两个文件中。

   >[!NOTE]
   >
   >使用 **ConfigurationManager.bat** 文件可帮助您避免手动更新.lax文件的名称。
   >

1. **[仅适用于基于Unix的]：**

   * 此 **启动Configuration Manager** 复选框默认处于选中状态。 单击 **[!UICONTROL 完成]** 立即运行配置管理器或运行 **配置管理器** 稍后，取消选择 **启动Configuration Manager** 选项，然后再单击 **[!UICONTROL 完成]**. 您可以开始 **配置管理器** 稍后使用中的相应脚本 `[AEM_forms_root]/configurationManager/bin` 目录。

1. 根据您的应用程序服务器，选择以下文档之一，然后按照 *配置和部署AEM表单* 部分。

   * [安装和部署AEM forms for JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [安装和部署AEM forms for WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (仅限JBoss®)安装修补程序并配置服务器后，删除JBoss®应用程序服务器的tmp和工作目录。

## 部署后配置 {#post-deployment-configurations}

### SAML配置 {#saml-configurations}

如果已配置SAML身份验证并且遇到大型IDP元数据问题，请在安装修补程序后执行以下操作：

1. 在应用程序服务器中设置以下系统属性：\
   `um.saml.enable.large.xml=true`
1. 重新启动服务器。
1. 按照SAML设置中的说明，删除现有的SAML身份验证提供程序，然后为现有域再次添加它们。

## 受影响的模块 {#impacted-modules}

* 文档服务
* 文档安全
* Foundation JEE

[联系支持人员](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support)
