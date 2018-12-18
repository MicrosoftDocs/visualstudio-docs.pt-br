---
title: Elemento SafeControl | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SafeControl element
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: aded7f246d961bd3f956611ff092dfdcf8b68564
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118352"
---
# <a name="safecontrol-element"></a>Elemento SafeControl
  Representa um controle ASPX ou a Web Part que é designado como seguro para qualquer usuário acessar em qualquer página ASPX no site do SharePoint.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<SafeControl Assembly = "Name of assembly that contains the safe control"  
    IsSafe = "true/false"  
    IsSafeAgainstScript = "true/false"  
    Name = "Name of this safe control entry"  
    Namespace = "Namespace of the safe control"  
    TypeName = "Type of the safe control" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|**Assembly**|Opcional **xs: string** atributo.<br /><br /> O nome do assembly no qual o controle ASPX ou a Web Part é definida. Por padrão, esse atributo usa o **$SharePoint.Project.AssemblyFullName$** parâmetro substituível para o nome do assembly. Para obter mais informações, consulte [parâmetros substituíveis](../sharepoint/replaceable-parameters.md).|  
|**IsSafe**|Opcional **xs: Boolean** atributo.<br /><br /> Especifica se o controle ASPX ou a Web Part é segura para usuários não confiáveis acessar.|  
|**IsSafeAgainstScript**|Opcional **xs: Boolean** atributo.<br /><br /> Especifica se os usuários não confiáveis podem exibir ou editar as propriedades do controle ASPX ou Web Part.|  
|**Nome**|Opcional **xs: string** atributo.<br /><br /> O nome desta entrada de controle seguro na coleção.|  
|**Namespace**|Opcional **xs: string** atributo.<br /><br /> O namespace do controle ASPX ou Web Part.|  
|**typeName**|Opcional **xs: string** atributo.<br /><br /> O nome do tipo do controle ASPX ou Web Part.|  
  
### <a name="child-elements"></a>Elementos filho
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[SafeControls](../sharepoint/safecontrols-element.md)|Representa uma coleção de controles ASPX e Web Parts que são designados como seguro para qualquer usuário acessar em qualquer página ASPX no site do SharePoint.|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre controles seguros, consulte [fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).  
  
## <a name="element-information"></a>Informações sobre o elemento
  
|||  
|-|-|  
|**Namespace**|HTTP<nolink>: //schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|  
|**Nome do esquema**|Esquema de Item de projeto do SharePoint|  
|**Arquivo de validação**|ProjectItemModelSchema.xsd|  
|**Pode estar vazio**|Não|  
  
## <a name="see-also"></a>Consulte também
 [Referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md)   
 [Fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)  
  
