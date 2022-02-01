---
title: 了解无标题内容以及如何在AEM中翻译
description: 了解无头概念、它们如何映射到AEM以及AEM翻译理论。
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# 了解无标题内容以及如何在AEM中翻译 {#learn-about}

了解无头概念、它们如何映射到AEM以及AEM翻译理论。

## 目标 {#objective}

本文档可帮助您了解无标题内容交付、AEM如何支持无标题内容，以及如何翻译此类内容。 阅读后，您应该：

* 了解无头内容交付的基本概念。
* 熟悉AEM如何支持无头和翻译。

## 全栈内容交付 {#full-stack}

自从易于使用的大型内容管理系统(CMS)兴起以来，各公司一直利用它们作为管理报文传送、品牌推广和通信的中心位置。 将CMS用作管理体验的中心点，通过消除在不同系统中重复任务的需要，提高了效率。

![经典的全栈CMS](/help/journey-headless/developer/assets/full-stack.png)

在全栈CMS中，用于处理内容的所有功能都在CMS中。 系统的功能构成了CMS堆栈的不同组件。 全栈解决方案具有许多优势。

* 有一个系统需要维护。
* 内容是集中管理的。
* 系统的所有服务都已集成。
* 内容创作是无缝的。

因此，如果必须添加新渠道或需要支持新类型的体验，则可以在堆栈中插入一个（或多个）新组件，并且只有一个位置进行更改。

![向堆栈中添加新渠道](/help/journey-headless/developer/assets/adding-channel.png)

但是，堆栈中依赖项的复杂性会很快变得明显，因为堆栈中的其他项目需要调整以适应更改。

## 无头的头 {#the-head}

任何系统的头通常是该系统的输出渲染器，通常以GUI或其他图形输出的形式。

当我们讨论无头CMS时，CMS会管理内容并继续向消费者提供内容。 但是，通过仅提供 **内容** 无头CMS以标准化方式忽略最终输出渲染，从而将 **演示文稿** 内容到消费服务。

![无头CMS](/help/journey-headless/developer/assets/headless-cms.png)

消费性服务(无论是AR体验、Web商店、移动体验、渐进式Web应用程序(PWA)等)从无头CMS中获取内容并提供自己的呈现。 他们负责为您的内容提供自己的头脑。

省略头部通过消除复杂性来简化CMS。 这样做还会将呈现内容的责任转移到实际需要内容且通常更适合此类呈现的服务上。

## 在AEM中翻译无标题内容 {#translating-in-aem}

除了提供强大的工具以全栈方式创建、管理和交付传统网页之外，AEM还提供创作内容的自含式选择并无头地提供这些内容的功能。

AEM的强大功能允许它无头、全栈或同时在两个模型中交付内容。 对于翻译专家而言，同一套翻译工具可以应用于这两种内容类型，从而为您提供了一种统一的内容翻译方法。

在历程中，您将进一步了解有关AEM如何翻译内容的详细信息，但在较高的层面，概念很简单：

1. 通过配置翻译集成框架定义与翻译服务的连接。
1. 定义应使用翻译规则翻译的内容。
1. 创建翻译项目以收集内容，将其发送到翻译服务并接收结果。
1. 审阅并发布翻译后的内容。

## 下一步 {#what-is-next}

感谢您开始使用AEM无头翻译历程！ 现在，您阅读了本文档，您应该：

* 了解无头内容交付的基本概念。
* 熟悉AEM如何支持无头和翻译。

在此知识的基础上，通过下一步审阅文档，继续您的AEM无头翻译历程 [AEM无头翻译入门](getting-started.md) 您将在此处概述AEM如何管理无头内容并了解其翻译工具。

## 其他资源 {#additional-resources}

但建议您通过审阅文档来进入无标题翻译历程的下一部分 [开始使用AEM无头翻译，](getting-started.md) 以下是一些其他可选资源，可更深入地了解本文档中提到的某些概念，但无需继续进行无头历程。

* [MSM和翻译](/help/sites-administering/msm-and-translation.md) - AEM多站点管理器的详细信息以及它如何与其翻译工具配合使用