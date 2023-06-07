---
title: JEE WebLogic服务器上的EAR部署失败
seo-title: EAR Deployment failing on JEE Weblogic Server
description: 解决JEE WebLogic服务器上的EAR部署失败的步骤
seo-description: Steps to resolve EAR Deployment failing on JEE Weblogic Server
source-git-commit: 45bb54a2666c2c196a8fb52795a7f428aa751e4d
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 6%

---


# JEE WebLogic服务器上的EAR部署失败 {#ear-deployment-failing-on-jee-weblogic-server}

## 问题 {#issue}

当用户尝试部署 `adobe-livecycle-weblogic.ear`，则 `Null Pointer` 遇到异常。

## 应用到 {#applies-to}

此解决方案适用于：

* WebLogic JEE服务器版本12.2.1.x上的AEM Forms。

## 解决方案 {#solution}

要解决此问题，请执行以下步骤：

1. 转到 `<domain_home>\bin` 已安装WebLogic JEE服务器的目录。

1. 编辑 `setDomainEnv.cmd` 或 `setDomainEnv.sh` 文件，作为 `applicable`.

1. 搜索最后一次出现的 `JAVA_OPTS` 并添加 `-DANTLR_USE_DIRECT_CLASS_LOADING=true` 敬它。 例如，更新的字符串显示为：

       set &#39;JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true&#39;
   
1. 保存更改。

