---
title: Elemento ProjectItem | Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItem element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 44fc1b918960f0268d916ccfa560f118cea47144
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536871"
---
# <a name="projectitem-element"></a>Elemento ProjectItem
  Representa um item de projeto do SharePoint. Esse elemento é o elemento raiz necessário do arquivo *. esdata* .

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
|**DefaultFile**|Atributo **xs: String** opcional.<br /><br /> O caminho relativo, incluindo o nome do arquivo, do arquivo que é aberto no editor do Visual Studio quando você abre o item de projeto do SharePoint no **Gerenciador de soluções**. O caminho é relativo a partir da pasta que contém o arquivo *. COMDATA* .|
|**FeatureReceiverClass**|Atributo **xs: String** opcional.<br /><br /> O nome totalmente qualificado de uma classe de receptor de recurso para este item de projeto do SharePoint. Para obter mais informações sobre os receptores de recursos, consulte [fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).|
|**FeatureReceiverAssembly**|Atributo **xs: String** opcional.<br /><br /> Especifica o nome totalmente qualificado de um assembly que define um receptor de recurso para este item de projeto do SharePoint. Para obter mais informações sobre os receptores de recursos, consulte [fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md). Para obter mais informações sobre nomes de assembly totalmente qualificados, consulte [nomes de assembly](/dotnet/framework/app-domains/assembly-names).|
|**SupportedTrustLevels**|Atributo **xs: String** opcional.<br /><br /> Especifica os níveis de confiança aos quais esse item de projeto do SharePoint dá suporte. Esse valor pode ser uma das seguintes cadeias de caracteres: Sandboxed, FullTrust ou ALL. O valor All especifica ambas as áreas restritas e FullTrust.<br /><br /> Em um tipo de item de projeto personalizado do SharePoint, o valor desse atributo corresponde ao valor que você atribui à <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A> propriedade em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> método. Se você especificar um valor diferente para esse atributo, o Visual Studio substituirá o valor para que ele especifique o mesmo nível de confiança que você especificar na <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A> propriedade.|
|**SupportedDeploymentScopes**|Atributo **xs: String** opcional.<br /><br /> Especifica os escopos de implantação aos quais esse item de projeto do SharePoint dá suporte. Esse valor é uma cadeia de caracteres delimitada por vírgula que consiste em uma ou mais das seguintes cadeias: Farm, site, Web, WebApplication ou pacote. Por exemplo: `Web, Site`<br /><br /> Em um tipo de item de projeto personalizado do SharePoint, o valor desse atributo corresponde ao valor que você atribui à <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A> propriedade em sua implementação do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> método. Se você especificar um valor diferente para esse atributo, o Visual Studio substituirá o valor para que ele especifique o mesmo nível de confiança que você especificar na <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A> propriedade.|
|**Tipo**|Atributo **xs: String** necessário.<br /><br /> O identificador do item de projeto do SharePoint. Em um tipo de item de projeto personalizado do SharePoint, o identificador é a cadeia de caracteres que você passa para o <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> . Para obter mais informações, consulte [como: definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md).<br /><br /> Para obter uma lista dos identificadores para os itens de projeto internos do SharePoint incluídos no Visual Studio, consulte [estender itens de projeto do SharePoint](../sharepoint/extending-sharepoint-project-items.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|Elemento opcional.<br /><br /> Representa uma coleção de itens de dados personalizados que estão associados ao item de projeto do SharePoint.<br /><br /> Você pode incluir apenas um elemento **ExtensionData** .|
|[Recursoproperties](../sharepoint/featureproperties-element.md)|Elemento opcional.<br /><br /> Representa uma coleção de valores de propriedade que são incluídos com um recurso quando ele é implantado no SharePoint.<br /><br /> Você pode incluir apenas um elemento **FeatureProperties** .|
|[Arquivos](../sharepoint/files-element.md)|Elemento **Filecollectiontype** opcional.<br /><br /> Especifica os arquivos a serem implantados com o item de projeto do SharePoint, como arquivos de elemento de recurso e a saída de projetos dependentes que não são do SharePoint.<br /><br /> Inclua **arquivos** ou um elemento **ProjectItemFolder** , mas não ambos.|
|[ProjectItemFolder](../sharepoint/projectitemfolder-element.md)|Elemento **ProjectItemFolderType** opcional.<br /><br /> Representa uma pasta mapeada.<br /><br /> Inclua **arquivos** ou um elemento **ProjectItemFolder** , mas não ambos.|
|[SafeControls](../sharepoint/safecontrols-element.md)|Elemento opcional.<br /><br /> Representa uma coleção de controles ASPX e Web Parts que são designados como seguros para qualquer usuário acessar em qualquer página ASPX no site do SharePoint.<br /><br /> Você pode incluir apenas um elemento **SafeControls** .|

### <a name="parent-elements"></a>Elementos pai
 Nenhum.

## <a name="element-information"></a>Informações do elemento

|Propriedade|Valor|
|-|-|
|**Namespace**|http: \/ \/ schemas.Microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**Nome do esquema**|Esquema de item de projeto do SharePoint|
|**Arquivo de validação**|ProjectItemModelSchema. xsd|
|**Pode estar vazio**|Não|

## <a name="see-also"></a>Confira também
[Rseference de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md)
