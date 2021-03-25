---
title: Elemento EnableLocationBrowseButton (modelos do Visual Studio)
description: Saiba mais sobre o elemento EnableLocationBrowseButton e como ele especifica se o botão procurar está disponível na caixa de diálogo novo projeto.
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#EnableLocationBrowseButton
helpviewer_keywords:
- EnableLocationBrowseButton [Visual Studio project templates]
ms.assetid: a12d10d8-af49-482a-af77-e084fd07a47d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5bf5ec98fc71158d9ebe3b95ec9e3d49526cb491
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061388"
---
# <a name="enablelocationbrowsebutton-element-visual-studio-templates"></a>Elemento EnableLocationBrowseButton (modelos do Visual Studio)
Especifica se o botão **procurar** está disponível na caixa de diálogo **novo projeto** , para que os usuários possam modificar facilmente o diretório padrão em que um novo projeto é salvo.

 \<VSTemplate> \<TemplateData>
 \<EnableLocationBrowseButton>

## <a name="syntax"></a>Sintaxe

```xml
<EnableLocationBrowseButton> true/false </EnableLocationBrowseButton>
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

 O texto deve ser `true` ou `false` , indicando se deseja ou não exibir o botão **procurar** na caixa de diálogo **novo projeto** .

## <a name="remarks"></a>Comentários
 `EnableLocationBrowseButton` é um elemento opcional. O valor padrão é `true` , que exibe o botão **procurar** na caixa de diálogo **novo projeto** .

 Na caixa de diálogo **novo projeto** , a caixa de texto **local** especifica o diretório em que um novo projeto é salvo. O botão **procurar** ajuda a modificar esse diretório exibindo a caixa de diálogo **local do projeto** , que permite que você navegue facilmente para um diretório diferente que está disponível no computador e, em seguida, escolha-o como o diretório no qual o novo projeto é salvo.

## <a name="example"></a>Exemplo
 O exemplo a seguir ilustra os metadados de um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] aplicativo do Windows.

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <EnableLocationBrowseButton>false</EnableLocationBrowseButton>
    </TemplateData>
    <TemplateContent>
        <Project File="MyStarterKit.csproj">
            <ProjectItem>Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>
            <ProjectItem>Properties\Resources.resx</ProjectItem>
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>
            <ProjectItem>Properties\Settings.settings</ProjectItem>
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>Confira também
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)
