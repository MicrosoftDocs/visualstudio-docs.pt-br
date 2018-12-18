---
title: Referência de esquema de Item de projeto do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FeatureProperty element
- SafeControls element
- SafeControl element
- .spdata files
- ExtensionData element
- FeatureProperties element
- ProjectOutputFile element
- Files element
- ProjectItemFolder element
- ProjectItemFile element
- ExtensionDataItem element
- ProjectItem element
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b94856d4e00cd15f324040ccd49c90bb1be29a7d
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118339"
---
# <a name="sharepoint-project-item-schema-reference"></a>Referência de esquema de item de projeto do SharePoint
  Visual Studio usa o esquema de item de projeto do SharePoint para validar o conteúdo de *. spdata* arquivos. Uma *. spdata* arquivo Especifica o conteúdo e o comportamento de um item de projeto do SharePoint. Para obter mais informações sobre o conteúdo de itens de projeto do SharePoint, consulte [criar um item modelos e modelos de projeto do SharePoint para itens de projeto](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).  
  
 O esquema de item de projeto do SharePoint é denominado ProjectItemModelSchema.xsd e é instalado por padrão em % arquivos de programas (x86)%\Microsoft Visual Studio 11.0\Xml\Schemas.  
  
 O elemento raiz é o [ProjectItem](../sharepoint/projectitem-element.md) elemento. A tabela a seguir descreve todos os elementos definidos pelo esquema.  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[ExtensionData](../sharepoint/extensiondata-element.md)|Representa uma coleção de itens de dados personalizados que estão associados com o item de projeto do SharePoint.|  
|[ExtensionDataItem](../sharepoint/extensiondataitem-element.md)|Representa um item de dados personalizado que está associado com o item de projeto do SharePoint, no formato de chave/valor. A chave e o valor devem ser cadeias de caracteres.|  
|[FeatureProperties](../sharepoint/featureproperties-element.md)|Representa uma coleção de valores de propriedade que são incluídos com um recurso quando ele é implantado no SharePoint. Depois que um recurso é implantado, você pode acessar os valores de propriedade em seu código.|  
|[FeatureProperty](../sharepoint/featureproperty-element.md)|Representa uma propriedade personalizada que está incluída com um recurso quando ele é implantado no SharePoint. Depois que um recurso é implantado, você pode acessar a propriedade em seu código.|  
|[Arquivos](../sharepoint/files-element.md)|Especifica os arquivos para implantar com o item de projeto do SharePoint, como um arquivo de elemento de recurso ou a saída de um projeto.|  
|[Item de projeto](../sharepoint/projectitem-element.md)|Representa um item de projeto do SharePoint.|  
|[ProjectItemFile](../sharepoint/projectitemfile-element.md)|Representa um arquivo do SharePoint, como o arquivo de elemento de recurso, para incluir com o item de projeto quando ele é implantado no SharePoint.|  
|[ProjectItemFolder](../sharepoint/projectitemfolder-element.md)|Representa uma pasta mapeada.|  
|[ProjectOutputFile](../sharepoint/projectoutputfile-element.md)|Representa a saída de um projeto para incluir com o item de projeto quando ele é implantado no SharePoint.|  
|[SafeControl](../sharepoint/safecontrol-element.md)|Representa um controle ASPX ou a Web Part que é designado como seguro para qualquer usuário acessar em qualquer página ASPX no site do SharePoint.|  
|[SafeControls](../sharepoint/safecontrols-element.md)|Representa uma coleção de controles ASPX e Web Parts que são designados como seguro para qualquer usuário acessar em qualquer página ASPX no site do SharePoint.|  
  
## <a name="see-also"></a>Consulte também
 [Criar modelos de projeto do SharePoint para itens de projeto e modelos de item](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)  
  
