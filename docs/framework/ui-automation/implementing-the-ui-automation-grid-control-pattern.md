---
title: "Implementing the UI Automation Grid Control Pattern | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "control patterns, grid"
  - "grid control pattern"
  - "UI Automation, grid control pattern"
ms.assetid: 234d11a0-7ce7-4309-8989-2f4720e02f78
caps.latest.revision: 27
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 27
---
# Implementing the UI Automation Grid Control Pattern
> [!NOTE]
>  本文档适用于想要使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 类的 .NET Framework 开发人员。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的最新信息，请参阅 [Windows 自动化 API：UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题介绍实现 <xref:System.Windows.Automation.Provider.IGridProvider> 的准则和约定，包括有关属性、方法和事件的信息。 本概述的结尾列出了指向其他参考资料的链接。  
  
 <xref:System.Windows.Automation.GridPattern> 控件模式用于支持作为子元素集合的容器的控件。 此元素的子元素必须实现 <xref:System.Windows.Automation.Provider.IGridItemProvider>，并且在可以按行和列进行遍历的二维逻辑坐标系统中进行组织。 有关实现此控件模式的控件示例，请参阅 [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## 实现准则和约定  
 在实现 Grid 控件模式时，请注意以下准则和约定：  
  
-   网格坐标从零开始，左上角单元格（或右上角单元格，具体取决于区域设置）的坐标为 \(0, 0\)。  
  
-   如果某个单元格为空，必须仍返回 UI 自动化元素以便支持该单元格的 <xref:System.Windows.Automation.Provider.IGridItemProvider.ContainingGrid%2A> 属性。 当网格中的子元素的布局类似于未对齐的数组时，这是可能的（请参阅下面的示例）。  
  
 ![显示未对齐布局的 Windows 资源管理器视图。](../../../docs/framework/ui-automation/media/uia-gridpattern-ragged-array.PNG "UIA\_GridPattern\_Ragged\_Array")  
坐标为空的 Grid 控件的示例  
  
-   只有一项的网格仍需要实现 <xref:System.Windows.Automation.Provider.IGridProvider>（如果它逻辑上被视为网格）。 网格中的子项数并不重要。  
  
-   隐藏的行和列（具体取决于提供程序实现）可能会在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树中加载，因此将会反映在 <xref:System.Windows.Automation.GridPattern.GridPatternInformation.RowCount%2A> 和 <xref:System.Windows.Automation.GridPattern.GridPatternInformation.ColumnCount%2A> 属性中。 如果尚未加载隐藏的行和列，则不应对它们进行计数。  
  
-   <xref:System.Windows.Automation.Provider.IGridProvider> 不会启用网格的主动操作；必须实现 <xref:System.Windows.Automation.Provider.ITransformProvider> 以启用此功能。  
  
-   使用 <xref:System.Windows.Automation.StructureChangedEventHandler> 来侦听对网格的结构和布局更改（如已添加、删除或合并的单元格）。  
  
-   使用 <xref:System.Windows.Automation.AutomationFocusChangedEventHandler> 来跟踪遍历的网格的项或单元格。  
  
<a name="Required_Members_for_IGridProvider"></a>   
## IGridProvider 必需的成员  
 实现 IGridProvider 接口需要以下属性和方法。  
  
|必需的成员|类型|备注|  
|-----------|--------|--------|  
|<xref:System.Windows.Automation.Provider.IGridProvider.RowCount%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.IGridProvider.ColumnCount%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.IGridProvider.GetItem%2A>|方法|无|  
  
 没有与此控件模式关联的事件。  
  
<a name="Exceptions"></a>   
## 异常  
 提供程序必须引发以下异常。  
  
|异常类型|条件|  
|----------|--------|  
|<xref:System.ArgumentOutOfRangeException>|<xref:System.Windows.Automation.Provider.IGridProvider.GetItem%2A><br /><br /> -   如果请求的行坐标大于 <xref:System.Windows.Automation.Provider.IGridProvider.RowCount%2A> 或列坐标大于 <xref:System.Windows.Automation.Provider.IGridProvider.ColumnCount%2A>。|  
|<xref:System.ArgumentOutOfRangeException>|<xref:System.Windows.Automation.Provider.IGridProvider.GetItem%2A><br /><br /> -   如果请求的行或列坐标任一个小于零。|  
  
## 请参阅  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [Implementing the UI Automation GridItem Control Pattern](../../../docs/framework/ui-automation/implementing-the-ui-automation-griditem-control-pattern.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)