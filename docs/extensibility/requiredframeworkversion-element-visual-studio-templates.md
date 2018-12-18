---
title: Elemento RequiredFrameworkVersion (modelos do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <RequiredFrameworkVersion> (Visual Studio Templates)
- RequiredFrameworkVersion (Visual Studio Templates)
ms.assetid: 08a4f609-51a5-4723-b89f-99277fb18871
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 23538e8e00553322f4f04e50414a8b3ddbd73b91
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39635906"
---
# <a name="requiredframeworkversion-element-visual-studio-templates"></a>Elemento RequiredFrameworkVersion (modelos do Visual Studio)

Especifica a versão mínima do .NET Framework que é exigido pelo modelo. Isso faz com que o **versão do Framework de destino** dropdown a ser exibido na **novo projeto** caixa de diálogo. O `RequiredFrameworkVersion` elemento também determina o valor mais baixo disponível na lista suspensa.

> [!IMPORTANT]
> A partir do Visual Studio 2017 versão 15.6, o **versão do Framework de destino** lista suspensa não é mais um filtro para os modelos exibidos na **modelos** seção o **novo projeto** caixa de diálogo. Em vez disso, a lista suspensa funciona como um seletor de estrutura para o modelo selecionado.

 \<VSTemplate > \<TemplateData > \<RequiredFrameworkVersion >

## <a name="syntax"></a>Sintaxe

```xml
<RequiredFrameworkVersion> .... </RequiredFrameworkVersion>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos
 nenhuma.

### <a name="child-elements"></a>Elementos filho
 nenhuma.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Elemento obrigatório.<br /><br /> Categoriza o modelo e a define como ele é exibido em qualquer um de **novo projeto** ou o **Adicionar Novo Item** caixa de diálogo.|

## <a name="text-value"></a>Valor de texto
 Um valor de texto é obrigatório.

 O texto deve ser o número de versão mínima do .NET Framework que é necessário para o modelo.

## <a name="remarks"></a>Comentários

`RequiredFrameworkVersion` é um elemento opcional. Use esse elemento somente se o modelo dá suporte a uma versão mínima específica (e versões posteriores, se houver) do .NET Framework. Se você especificar o `RequiredFrameworkVersion` elemento e seu modelo não dá suporte a uma versão específica de mínima do .NET Framework, o **versão do Framework de destino** menu suspenso é exibido quando não é aplicável.

## <a name="example"></a>Exemplo

O exemplo a seguir ilustra os metadados para um padrão [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] modelo de classe.

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

Neste exemplo, a versão mínima do .NET Framework que é exigido pelo modelo, representado por `RequiredFrameworkVersion`, é 3.0. Um projeto criado com esse modelo pode direcionar o .NET Framework 3.0 a partir de versões.

## <a name="see-also"></a>Consulte também

- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Uma versão específica do .NET Framework de destino](../ide/targeting-a-specific-dotnet-framework-version.md)
