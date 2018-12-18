---
title: Elemento ProjectItem | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItem element
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ca0c295410caffb476d6c1e796864c47520a2f56
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118545"
---
# <a name="projectitem-element"></a>Elemento ProjectItem
  Representa um item de projeto do SharePoint. Esse elemento o elemento raiz necessário do *. spdata* arquivo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<ProjectItem DefaultFile = "File that opens in the editor when you open the project item"  
    FeatureReceiverClass = "Class that implements a feature receiver for the project item"  
    FeatureReceiverAssembly = "Assembly that defines a feature receiver for the project item"  
    SupportedTrustLevels = "Trust levels that the project item supports"  
    SupportedDeploymentScopes = "Deployment scopes that the project item supports"  
    Type="Identifier for the project item">  
  <Files>...</Files>  
  <ProjectItemFolder>...</ProjectItemFolder>  
  <SafeControls>...</SafeControls>  
  <FeatureProperties>...</FeatureProperties>  
  <ExtensionData>...</ExtensionData>  
</ProjectItem>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|**DefaultFile**|Opcional **xs: string** atributo.<br /><br /> O caminho relativo, incluindo o nome de arquivo, do arquivo que é aberto no editor do Visual Studio quando você abre o item de projeto do SharePoint no **Gerenciador de soluções**. O caminho é relativo da pasta que contém o *. spdata* arquivo.|  
|**FeatureReceiverClass**|Opcional **xs: string** atributo.<br /><br /> O nome totalmente qualificado de uma classe de receptor de recurso para este item de projeto do SharePoint. Para obter mais informações sobre os receptores de recurso, consulte [fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).|  
|**FeatureReceiverAssembly**|Opcional **xs: string** atributo.<br /><br /> Especifica o nome totalmente qualificado de um assembly que define um receptor de recurso para este item de projeto do SharePoint. Para obter mais informações sobre os receptores de recurso, consulte [fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md). Para obter mais informações sobre nomes de assembly totalmente qualificado, consulte [nomes de Assembly](/dotnet/framework/app-domains/assembly-names).|  
|**SupportedTrustLevels**|Opcional **xs: string** atributo.<br /><br /> Especifica os níveis de confiança que dá suporte a esse item de projeto do SharePoint. Esse valor pode ser uma das seguintes cadeias de caracteres: área restrita, FullTrust, ou tudo. O valor All Especifica Sandboxed e FullTrust.<br /><br /> Em um tipo de item de projeto do SharePoint personalizado, o valor desse atributo corresponde ao valor que você atribui para a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A> propriedade em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> método. Se você especificar um valor diferente para esse atributo, o Visual Studio substitui o valor para que ele especifique o mesmo nível de confiança que você especificar na <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A> propriedade.|  
|**SupportedDeploymentScopes**|Opcional **xs: string** atributo.<br /><br /> Especifica os escopos de implantação que dá suporte a esse item de projeto do SharePoint. Esse valor é uma cadeia de caracteres delimitada por vírgula que consiste em uma ou mais das seguintes cadeias de caracteres: Farm, Site, Web, aplicativo Web ou pacote. Por exemplo: `Web, Site`<br /><br /> Em um tipo de item de projeto do SharePoint personalizado, o valor desse atributo corresponde ao valor que você atribui para a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A> propriedade em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> método. Se você especificar um valor diferente para esse atributo, o Visual Studio substitui o valor para que ele especifique o mesmo nível de confiança que você especificar na <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A> propriedade.|  
|**Tipo**|Exigido **xs: string** atributo.<br /><br /> O identificador do item de projeto do SharePoint. Em um tipo de item de projeto do SharePoint personalizado, o identificador é a cadeia de caracteres que você passa para o <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. Para obter mais informações, consulte [como: definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md).<br /><br /> Para obter uma lista dos identificadores para os itens de projeto do SharePoint internos incluídos no Visual Studio, consulte [itens de projeto do SharePoint estender](../sharepoint/extending-sharepoint-project-items.md).|  
  
### <a name="child-elements"></a>Elementos filho
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[ExtensionData](../sharepoint/extensiondata-element.md)|Elemento opcional.<br /><br /> Representa uma coleção de itens de dados personalizados que estão associados com o item de projeto do SharePoint.<br /><br /> Você pode incluir apenas uma **ExtensionData** elemento.|  
|[FeatureProperties](../sharepoint/featureproperties-element.md)|Elemento opcional.<br /><br /> Representa uma coleção de valores de propriedade que são incluídos com um recurso quando ele é implantado no SharePoint.<br /><br /> Você pode incluir apenas uma **FeatureProperties** elemento.|  
|[Arquivos](../sharepoint/files-element.md)|Opcional **FileCollectionType** elemento.<br /><br /> Especifica os arquivos para implantar com o item de projeto do SharePoint, como arquivos de recurso de elemento e a saída de projetos do SharePoint não dependentes.<br /><br /> Incluir um **arquivos** ou um **ProjectItemFolder** elemento, mas não ambos.|  
|[ProjectItemFolder](../sharepoint/projectitemfolder-element.md)|Opcional **ProjectItemFolderType** elemento.<br /><br /> Representa uma pasta mapeada.<br /><br /> Incluir um **arquivos** ou um **ProjectItemFolder** elemento, mas não ambos.|  
|[SafeControls](../sharepoint/safecontrols-element.md)|Elemento opcional.<br /><br /> Representa uma coleção de controles ASPX e Web Parts que são designados como seguro para qualquer usuário acessar em qualquer página ASPX no site do SharePoint.<br /><br /> Você pode incluir apenas uma **SafeControls** elemento.|  
  
### <a name="parent-elements"></a>Elementos pai
 nenhuma.  
  
## <a name="element-information"></a>Informações sobre o elemento
  
|||  
|-|-|  
|**Namespace**|HTTP<nolink>: //schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|  
|**Nome do esquema**|Esquema de Item de projeto do SharePoint|  
|**Arquivo de validação**|ProjectItemModelSchema.xsd|  
|**Pode estar vazio**|Não|  
  
## <a name="see-also"></a>Consulte também
[Rseference de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md)  
  
