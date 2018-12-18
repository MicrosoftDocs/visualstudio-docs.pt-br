---
title: Elemento MaxFrameworkVersion (modelos do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <MaxFrameworkVersion> Element (Visual Studio Templates)
- MaxFrameworkVersion Element (Visual Studio Templates)
ms.assetid: f732a9d3-fc29-405b-9298-01ea83fc58b8
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 12433fd96aee78c0f8f9ead3b531ae11b1d28f17
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39636354"
---
# <a name="maxframeworkversion-element-visual-studio-templates"></a>Elemento MaxFrameworkVersion (modelos do Visual Studio)

Especifica a versão máxima do .NET Framework que é necessário para o modelo. Determina o valor mais alto disponível na **versão do Framework de destino** dropdown do **novo projeto** caixa de diálogo. Em ordem para que os usuários possam selecionar uma versão do framework, você também deve especificar [RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md) como a versão mínima do .NET Framework para o modelo.

> [!IMPORTANT]
> A partir do Visual Studio 2017 versão 15.6, o **versão do Framework de destino** lista suspensa não é mais um filtro para os modelos exibidos na **modelos** seção o **novo projeto** caixa de diálogo. Em vez disso, o **versão do Framework de destino** suspensa funciona como um seletor de estrutura para o modelo selecionado.

 \<VSTemplate > \<TemplateData > \<MaxFrameworkVersion >

## <a name="syntax"></a>Sintaxe

```xml
<MaxFrameworkVersion> ... </MaxFrameworkVersion>
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

 O texto deve ser o maior número de versão do .NET Framework que é permitido pelo modelo.

## <a name="remarks"></a>Comentários

`MaxFrameworkVersion` é um elemento opcional. O `MaxFrameworkVersion` elemento deve ser omitido, a menos que é necessário, assim como não inadvertidamente limitar as versões de intervalo com suporte do .NET Framework para o modelo. Ele também deverá ser omitido se o .NET Framework não é aplicável ao modelo.

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

Neste exemplo, a versão máxima do .NET Framework que é exigido pelo modelo, representado por `MaxFrameworkVersion`, é de 4.7.1. Um projeto criado com esse modelo pode direcionar versões do .NET Framework até 4.7.1.

## <a name="see-also"></a>Consulte também

- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
