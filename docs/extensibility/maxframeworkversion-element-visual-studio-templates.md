---
title: Elemento MaxFrameworkVersion (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento MaxFrameworkVersion e como ele especifica a versão máxima do .NET Framework exigido pelo modelo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <MaxFrameworkVersion> Element (Visual Studio Templates)
- MaxFrameworkVersion Element (Visual Studio Templates)
ms.assetid: f732a9d3-fc29-405b-9298-01ea83fc58b8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 05d61e298c666d22df1af8d426cb0671feb8b9c5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090610"
---
# <a name="maxframeworkversion-element-visual-studio-templates"></a>Elemento MaxFrameworkVersion (modelos do Visual Studio)

Especifica a versão máxima do .NET Framework exigido pelo modelo. Ele determina o maior valor disponível no menu suspenso **versão da estrutura de destino** da caixa de diálogo **novo projeto** . Para que os usuários possam selecionar uma versão de estrutura, você também deve especificar [RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md) como a versão de .NET Framework mínima para o modelo.

> [!IMPORTANT]
> A partir do Visual Studio 2017 versão 15,6, o menu suspenso **versão da estrutura de destino** não é mais um filtro para modelos exibidos na seção **modelos** da caixa de diálogo **novo projeto** . Em vez disso, o menu suspenso **versão da estrutura de destino** funciona como um seletor de estrutura para o modelo selecionado.

 \<VSTemplate> \<TemplateData>
 \<MaxFrameworkVersion>

## <a name="syntax"></a>Sintaxe

```xml
<MaxFrameworkVersion> ... </MaxFrameworkVersion>
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

 O texto deve ser o número de versão mais alto do .NET Framework permitido pelo modelo.

## <a name="remarks"></a>Comentários

`MaxFrameworkVersion` é um elemento opcional. O `MaxFrameworkVersion` elemento deve ser omitido, a menos que seja necessário, portanto, não limitar inadvertidamente o intervalo com suporte de versões de .NET Framework para o modelo. Ele também deverá ser omitido se .NET Framework não for aplicável ao modelo.

## <a name="example"></a>Exemplo

O exemplo a seguir ilustra os metadados para um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] modelo de classe padrão.

```xml
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class template.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>3.0</RequiredFrameworkVersion>
        <MaxFrameworkVersion>4.7.1</MaxFrameworkVersion>
        <DefaultName>MyClass</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem>MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

Neste exemplo, a versão máxima do .NET Framework exigido pelo modelo, representada por `MaxFrameworkVersion` , é 4.7.1. Um projeto criado com este modelo pode ter como destino .NET Framework versões até o 4.7.1.

## <a name="see-also"></a>Confira também

- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)
