---
description: Especifica a versão mínima do .NET Framework exigido pelo modelo.
title: Elemento RequiredFrameworkVersion (modelos do Visual Studio)
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <RequiredFrameworkVersion> (Visual Studio Templates)
- RequiredFrameworkVersion (Visual Studio Templates)
ms.assetid: 08a4f609-51a5-4723-b89f-99277fb18871
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 661e4067ac0191444be8ec7f1136f805ea8b39b5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068447"
---
# <a name="requiredframeworkversion-element-visual-studio-templates"></a>Elemento RequiredFrameworkVersion (modelos do Visual Studio)

Especifica a versão mínima do .NET Framework exigido pelo modelo. Ele faz com que a lista suspensa da **versão do Framework de destino** seja exibida na caixa de diálogo **novo projeto** . O `RequiredFrameworkVersion` elemento também determina o menor valor disponível na lista suspensa.

> [!IMPORTANT]
> A partir do Visual Studio 2017 versão 15,6, o menu suspenso **versão da estrutura de destino** não é mais um filtro para modelos exibidos na seção **modelos** da caixa de diálogo **novo projeto** . Em vez disso, as funções suspensas como um seletor de estrutura para o modelo selecionado.

 \<VSTemplate> \<TemplateData>
 \<RequiredFrameworkVersion>

## <a name="syntax"></a>Sintaxe

```xml
<RequiredFrameworkVersion> .... </RequiredFrameworkVersion>
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

 O texto deve ser o número de versão mínimo do .NET Framework necessário para o modelo.

## <a name="remarks"></a>Comentários

`RequiredFrameworkVersion` é um elemento opcional. Use esse elemento somente se o modelo oferecer suporte a uma versão mínima específica (e versões posteriores, se houver) da .NET Framework. Se você especificar o `RequiredFrameworkVersion` elemento e o modelo não oferecer suporte a uma versão mínima específica do .NET Framework, a lista suspensa **versão do Framework de destino** será exibida quando não for aplicável.

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

Neste exemplo, a versão mínima do .NET Framework exigido pelo modelo, representada por `RequiredFrameworkVersion` , é 3,0. Um projeto criado com este modelo pode se destinar a versões .NET Framework a partir de 3,0.

## <a name="see-also"></a>Confira também

- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Visão geral do direcionamento de estrutura](../ide/visual-studio-multi-targeting-overview.md)
