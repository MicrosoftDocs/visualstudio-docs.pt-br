---
title: Elemento SafeControl | Microsoft Docs
description: Obtenha informações sobre o elemento SafeControl, que representa um controle ASPX ou Web Part marcado como seguro para que um usuário acesse na página ASPX de um site do SharePoint.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SafeControl element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 36a8b0ed45fbdb8d2dfe8e93a027a47adf407587
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "95440617"
---
# <a name="safecontrol-element"></a>Elemento SafeControl
  Representa um controle ASPX ou Web Part designado como seguro para qualquer usuário acessar em qualquer página ASPX no site do SharePoint.

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
|**Assembly**|Atributo **xs: String** opcional.<br /><br /> O nome do assembly no qual o controle ASPX ou Web Part é definido. Por padrão, esse atributo usa o parâmetro **$SharePoint. Project. AssemblyFullName $** substituível para o nome do assembly. Para obter mais informações, consulte [parâmetros substituíveis](../sharepoint/replaceable-parameters.md).|
|**IsSafe**|Atributo **xs: Boolean** opcional.<br /><br /> Especifica se o controle ASPX ou Web Part é seguro para usuários não confiáveis acessarem.|
|**IsSafeAgainstScript**|Atributo **xs: Boolean** opcional.<br /><br /> Especifica se os usuários não confiáveis podem exibir ou editar as propriedades do controle ASPX ou Web Part.|
|**Nome**|Atributo **xs: String** opcional.<br /><br /> O nome desta entrada de controle seguro na coleção.|
|**Namespace**|Atributo **xs: String** opcional.<br /><br /> O namespace do controle ASPX ou Web Part.|
|**TypeName**|Atributo **xs: String** opcional.<br /><br /> O nome do tipo do controle ASPX ou Web Part.|

### <a name="child-elements"></a>Elementos filho
 Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[SafeControls](../sharepoint/safecontrols-element.md)|Representa uma coleção de controles ASPX e Web Parts que são designados como seguros para qualquer usuário acessar em qualquer página ASPX no site do SharePoint.|

## <a name="remarks"></a>Comentários
 Para obter mais informações sobre controles seguros, consulte [fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).

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
