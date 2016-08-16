---
layout: post
title:  "How Google Test"
subtitle: "读书笔记"
date:   2016-08-16 19:33:32 +0800
categories: 测试
author:     "Wenxi"
tags:
    - 读书笔记
    - 测试
---

《Google软件测试之道－像Google一样进行软件测试》是阿里巴巴三位技术专家翻译的，难怪读起来感觉跟阿里巴巴的招聘要求一样。

本书分五章：第1章Google软件测试介绍；第2章软件测试开发工程师；第3章测试工程师；第4章测试工程经理；第5章Google软件测试改进。有三章是“人”，表面看起来是讲不同角色的测试范围，其实是由浅入深将测试思维。

## 第1章 Google软件测试介绍

根据测试范围和关注对象，本书将测试角色分为3类：

. 软件开发工程师SWE(software engineer)

. 软件测试开发工程师SET(software engineer in test)

. 测试工程师TE(test engineer)

SWE是一个传统上的开发角色，主要工作是实现最终用户所使用的功能代码。SWE也需要编写测试代码，包括测试驱动的设计、单元测试、参与构建各种大小规模的测试等。

SET也是开发角色，只是工作重心在可测试性和通用测试基础框架上。SET编写单元测试框架和自动化测试框架。SET的主要关注对象就是开发人员，SET的主要职责是让开发者可以很容易地编写测试代码，从而达到独立功能模块的质量要求。SWE和SET要确认做了足够多的模块级别与功能级别的测试。

TE把用户放在第一位来思考，TE组织整体质量实践，分析解释测试运行结果，驱动测试执行，构建端到端的自动化测试。TE的职责是专注于用户角度的测试，TE扮演着一个双重确认的角色，一方面确认开发人员在测试方面的工作是否到位，另一方面会把注意力转移到用户使用场景中，是否满足性能期望，在安全性、国际化、访问权限等方面是否满足用户的要求。

## 第2章 软件测试开发工程师

理论上，在面试SET的时候，在代码要求标准上与SWE的招聘要求是一样的，而且增加了额外考核——SET需要了解如何去测试他们编写的代码。找到满足这些条件的人非常困难，连Google也没有完全做到。我听说阿里巴巴正在向这个方向转型，要求测试人员具有开发能力，估计这也是软件测试向上发展的趋势。

SET什么时间介入项目，以及介入项目之后做些什么工作？在这一章节会有讲解。像Google这样很多产品时业余时间创新产生的，在产品概念还没完全定型之前，没有特别强调测试。“只有在软件产品变得重要的时候质量才显得重要”。SET初期就加入了项目是比较好的，SET的巨大优势就是拥有产品方面最广阔的视野。通常来说，代码复用和模块交互方面的设计会由SET来做，而不是SWE。

书上的理论时这样讲，我猜测实际开发中，产品经理负责了产品方面最广阔的视野，代码复用和模块交互估计也不是有SET来设计。项目初期更多的估计还是写文档，设计用例，所以啊，理论和现实的差距还是蛮远的。

SET时间有限且需要做的事情太多，尽早地提供一个可实施的自动化测试计划是一个很好的解决办法。此时要避免一个常见的错误，试图在一个测试套件中自动化所有端到端的测试用例。在端到端自动化测试上过度投入，常常会把你的产品的特定功能设计绑定在一起。在Google，SET遵循了下面的方法。首先把容易出错的接口做隔离，并针对它们创建mock和fake。接下来构建一个轻量级的自动化框架，控制mock系统的创建和执行。

关于测试大小的定义，Google不是按单元测试、代码级别测试、白盒测试、集成测试、系统测试、端到端测试来分的，而是分为小型测试、中型测试、大型测试。每一种测试规模都带来一些益处，小型测试带来优秀的代码质量、良好的异常处理、优雅的错误报告；大型中型测试会带来整体产品质量和数据验证。小型测试、中型测试、大型测试之间的比例，Google有一个经验法则，即70/20/10原则：70%是小型测试，20%是中型测试，10%是大型测试。


待补充……