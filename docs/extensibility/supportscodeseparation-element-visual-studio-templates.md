---
title: Elemento SupportsCodeSeparation (modelos do Visual Studio)
titleSuffix: ''
description: Saiba mais sobre o elemento SupportsCodeSeparation e como ele especifica se a caixa de seleção posicionar código em um arquivo separado está habilitada na caixa de diálogo Adicionar novo item.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SupportsCodeSeparation
helpviewer_keywords:
- SupportsCodeSeparation element [Visual Studio Templates]
- <SupportsCodeSeparation> element [Visual Studio Templates]
ms.assetid: 8112aac8-a269-40e5-b92b-9b9a6ff5a542
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 699d38f712885d1e2b08a111baa7db75fb7829da
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056123"
---
# <a name="supportscodeseparation-element-visual-studio-templates"></a>Elemento SupportsCodeSeparation (modelos do Visual Studio)
Especifica se a caixa de seleção **código local em arquivo separado** está habilitada na caixa de diálogo **Adicionar novo item** .

 \<VSTemplate> \<TemplateData>
 \<SupportsCodeSeparation>

## <a name="syntax"></a>Sintaxe

```
<SupportsCodeSeparation> true/false </SupportsCodeSeparation>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Elemento necessário.<br /><br /> Categoriza o modelo e define como ele é exibido na caixa de diálogo **novo projeto** ou **novo item** .|

## <a name="text-value"></a>Valor de texto
 Um valor de texto é obrigatório.

 O texto deve ser `true` ou `false` , indicando se a caixa de seleção **código local em arquivo separado** está habilitada na caixa de diálogo **Adicionar novo item** .

## <a name="remarks"></a>Comentários
 `SupportsCodeSeparation` é um elemento opcional. O valor padrão é `false`.

 O `SupportsCodeSeparation` elemento só está disponível para modelos de item da Web.

 A separação de código ou o modelo de página code-behind permite que você mantenha a marcação em um arquivo e o código de programação em outro arquivo. [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] e outras linguagens .NET usam esse modelo.

## <a name="example"></a>Exemplo
 O exemplo a seguir especifica a exibição do **código do local em uma opção de arquivo separado** .

```
<VSTemplate Version="3.0.0" Type="Project"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">>
    <TemplateData>
        <Name>MyWebProjecStarterKit</Name>
        <Description>A simple Web template</Description>
        <Icon>icon.ico</Icon>
        <ProjectType>Web</ProjectType>
        <ProjectSubType>CSharp</ProjectSubType>
        <DefaultName>WebSite</DefaultName>
        <SupportsCodeSeparation>true</SupportsCodeSeparation>
    </TemplateData>
    <TemplateContent>
        <Project File="WebApplication.webproj">
            <ProjectItem>icon.ico</ProjectItem>
            <ProjectItem OpenInEditor="true">Default.aspx</ProjectItem>
            <ProjectItem>Default.aspx.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>Confira também
- [Referência de esquema do modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
