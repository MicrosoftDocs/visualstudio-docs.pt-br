---
title: Elemento ProvideDefaultName (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento ProvideDefaultName e como ele especifica se o Visual Studio irá gerar um nome do Visual Studio padrão na caixa de diálogo Adicionar novo item ou novo projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProvideDefaultName
helpviewer_keywords:
- ProvideDefaultName element [Visual Studio project templates]
ms.assetid: 7b0e7b20-fd6b-42e2-81d0-e5100cea0528
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d29ca3075ee6e5ef031bb360ecfd10d6cb341c26
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068629"
---
# <a name="providedefaultname-element-visual-studio-templates"></a>Elemento ProvideDefaultName (modelos do Visual Studio)
Especifica se o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] sistema do projeto irá gerar um nome padrão para o modelo na caixa de diálogo **Adicionar novo item** ou **novo projeto** .

 \<VSTemplate> \<TemplateData>
 \<ProvideDefaultName>

## <a name="syntax"></a>Sintaxe

```xml
<ProvideDefaultName> true/false </ProvideDefaultName>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos
 Nenhum.

### <a name="child-elements"></a>Elementos filho
 Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Elemento necessário.<br /><br /> Categoriza o modelo e define como ele é exibido no **novo projeto** ou na caixa de diálogo **Adicionar novo item** .|

## <a name="text-value"></a>Valor de texto
 Um valor de texto é obrigatório.

 O texto deve ser `true` ou `false` , indicando se deve ou não gerar um nome padrão para o modelo na caixa de **diálogo Adicionar novo item** ou **novo projeto** .

## <a name="remarks"></a>Comentários
 `ProvideDefaultName` é um elemento opcional. O valor padrão é `true`.

 Se o `ProvideDefaultName` elemento for `false` , as caixas de **nome** das caixas de diálogo **Adicionar novo item** e **novo projeto** conterá o valor `<Enter_name>` .

 Use o elemento [DefaultName](../extensibility/defaultname-element-visual-studio-templates.md) para especificar o nome padrão do projeto ou do item nas caixas de diálogo **Adicionar novo item** e **novo projeto** . Quando o valor do `ProvideDefaultName` elemento é `true` , a omissão do `DefaultName` elemento para projetos popula a caixa de diálogo com o nome do modelo, ou seja, o valor do elemento [Name](../extensibility/name-element-visual-studio-templates.md) .

## <a name="example"></a>Exemplo
 O exemplo de código a seguir define o `ProvideDefaultName` elemento como `false` .

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <ProvideDefaultName>false</ProvideDefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem>MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>Confira também
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
