---
title: "&lt;特性暗示&gt;元素 (.NET Native) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 82db7193-a860-418b-84fc-fff2fdf2e025
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# &lt;特性暗示&gt;元素 (.NET Native)
为包含特性应用的代码元素定义策略。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributeImplies Activate="policy_type"  
                  Browse="policy_type"  
                  Dynamic="policy_type"  
                  Serialize="policy_type"   
                  DataContractSerializer="policy_setting"  
                  DataContractJsonSerializer="policy_setting"  
                  XmlSerializer="policy_setting"  
                  MarshalObject="policy_setting"  
                  MarshalDelegate="policy_setting"  
                  MarshalStructure="policy_setting" />  
  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|特性类型|说明|  
|---------------|--------------------|-----------------|  
|`Activate`|映像|可选特性。 控制运行时对构造函数的访问，以启用实例激活。|  
|`Browse`|映像|可选特性。 控制对有关程序元素信息的查询，但并不启用任何运行时访问。|  
|`Dynamic`|映像|可选特性。 控制运行时对所有类型成员的访问，包括构造函数、方法、字段、属性和事件，以启用动态编程。|  
|`Serialize`|序列化|可选特性。 控制运行时对构造函数、字段和属性的访问，使类型实例得到序列化和反序列化处理，这是通过库进行的，例如 Newtonsoft JSON 序列化程序。|  
|`DataContractSerializer`|序列化|可选特性。 控制使用的序列化策略<xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName>类。|  
|`DataContractJsonSerializer`|序列化|可选特性。 控制使用的 JSON 序列化策略<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=fullName>类。|  
|`XmlSerializer`|序列化|可选特性。 控制使用的 XML 序列化策略<xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName>类。|  
|`MarshalObject`|Interop|可选特性。 控制封送引用类型到 Windows 运行时和 COM 的策略。|  
|`MarshalDelegate`|Interop|可选特性。 控制将委托类型作为函数指针封送到本机代码的策略。|  
|`MarshalStructure`|Interop|可选特性。 控制封送处理值类型到本机代码的策略。|  
  
## <a name="all-attributes"></a>所有特性  
  
|值|描述|  
|-----------|-----------------|  
|*policy_setting*|该设置将应用到这种策略类型。 可能值为 `All`、`Auto`、`Excluded`、`Public`、`PublicAndInternal`、`Required Public`、`Required PublicAndInternal` 以及 `Required All`。 有关详细信息，请参阅[运行时指令策略设置](../../../docs/framework/net-native/runtime-directive-policy-settings.md)。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/type-element-net-native.md)|将反射策略应用到一种类型及其所有成员。|  
  
## <a name="remarks"></a>备注  
 `<AttributeImplies>`如果其包含类型是一个特性，则使用元素 (从派生的类，即<xref:System.Attribute?displayProperty=fullName>)。 如果该特性被应用到特定的程序元素，由 `<AttributeImplies>` 元素定义的策略将应用到该程序元素。  
  
 反射、序列化和互操作特性都是可选项，但必须存在至少一项。  
  
## <a name="see-also"></a>另请参阅  
 [<>\>元素](../../../docs/framework/net-native/type-element-net-native.md)   
 [运行时指令 (rd.xml) 配置文件引用](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [运行时指令元素](../../../docs/framework/net-native/runtime-directive-elements.md)   
 [运行时指令策略设置](../../../docs/framework/net-native/runtime-directive-policy-settings.md)