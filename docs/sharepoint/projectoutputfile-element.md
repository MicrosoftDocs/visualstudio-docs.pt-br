---
title: Elemento ProjectOutputFile | Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectOutputFile element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 12f399b7a09c18c77482475575ca387a11955762
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542383"
---
# <a name="projectoutputfile-element"></a>Elemento ProjectOutputFile
  Representa a saída de um projeto separado a ser incluído com o item de projeto quando ele é implantado no SharePoint.

## <a name="syntax"></a>Sintaxe

```xml
<ProjectOutputFile ProjectId = "GUID of the project"
    ProjectPath = "Relative path of the project"
    Target = "Deployment path of the project output"
    Type = "Type of deployment for the project output" />
```

## <a name="type"></a>Type
 **ProjectOutputFileType**

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|**ProjectId**|Atributo **xs: String** necessário.<br /><br /> O GUID do projeto dependente que tem a saída que você deseja incluir. Isso corresponde ao elemento **ProjectGuid** no arquivo de projeto dependente.|
|**ProjectPath**|Atributo **xs: String** necessário.<br /><br /> O caminho relativo, incluindo o nome do arquivo de projeto, do projeto dependente que tem a saída que você deseja incluir. Esse caminho é relativo à pasta raiz do projeto do SharePoint que contém o item de projeto do SharePoint.|
|**Destino**|Atributo **xs: String** opcional.<br /><br /> O caminho em que a saída do projeto dependente deve ser implantada no servidor do SharePoint, em relação à pasta raiz da implantação. A pasta raiz de implantação é determinada pelo tipo de implantação especificado pelo atributo de **tipo** .<br /><br /> Para obter mais informações, consulte as descrições das propriedades **caminho de implantação** e raiz de **implantação** dos itens de projeto do SharePoint em [desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md).|
|**Tipo**|Atributo **xs: String** necessário.<br /><br /> O tipo de implantação a ser usado para a saída do projeto dependente. Para obter mais informações sobre os valores possíveis, consulte a descrição para a propriedade **tipo de implantação** de itens de projeto do SharePoint em [desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md).|

### <a name="child-elements"></a>Elementos filho
 Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Arquivos](../sharepoint/files-element.md)|Especifica os arquivos a serem incluídos com o item de projeto do SharePoint quando ele é implantado no SharePoint.|

## <a name="remarks"></a>Comentários
 Use o elemento **ProjectOutputFile** para incluir a saída de um projeto na implantação do item de projeto do SharePoint. Você pode especificar um projeto diferente ou o mesmo projeto que contém o item de projeto. Para obter mais informações, consulte [fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).

## <a name="element-information"></a>Informações do elemento

|Propriedade|Valor|
|-|-|
|**Namespace**|http: \/ \/ schemas.Microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**Nome do esquema**|Esquema de item de projeto do SharePoint|
|**Arquivo de validação**|ProjectItemModelSchema. xsd|
|**Pode estar vazio**|Não|

## <a name="see-also"></a>Confira também
- [Referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md)
- [Fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
