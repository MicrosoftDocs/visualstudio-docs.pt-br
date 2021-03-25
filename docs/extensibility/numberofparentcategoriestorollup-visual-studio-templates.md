---
title: Elemento NumberOfParentCategoriesToRollUp (modelos)
description: Saiba mais sobre o elemento NumberOfParentCategoriesToRollUp e como ele especifica o número de categorias pai que exibirão o modelo na caixa de diálogo novo projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#NumberOfParentCategoriesToRollUp
helpviewer_keywords:
- NumberOfParentCategoriesToRollUp element [Visual Studio Templates]
- <NumberOfParentCategoriesToRollUp> element [Visual Studio Templates]
ms.assetid: 6f9d36f5-ae23-4a92-8132-b11799e2c21a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 02c6f0e22429b268fb643c622ebd1f237a4721d3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090467"
---
# <a name="numberofparentcategoriestorollup-element-visual-studio-templates"></a>Elemento NumberOfParentCategoriesToRollUp (modelos do Visual Studio)
Especifica o número de categorias pai que exibirá o modelo na caixa de diálogo **novo projeto** .

 \<VSTemplate> \<TemplateData>
 \<NumberOfParentCategoriesToRollUp>

## <a name="syntax"></a>Sintaxe

```xml
<NumberOfParentCategoriesToRollUp>
1
</NumberOfParentCategoriesToRollUp>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Categoriza o modelo e define como ele é exibido no **novo projeto** ou na caixa de diálogo **Adicionar novo item** .|

## <a name="text-value"></a>Valor de texto
 `integer`É necessário um valor.

 Esse valor especifica o número de categorias pai que exibirá o modelo na caixa de diálogo **novo projeto** .

## <a name="remarks"></a>Comentários
 `NumberOfParentCategoriesToRollUp` é um elemento opcional.

## <a name="example"></a>Exemplo
 Este exemplo ilustra os metadados de um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] aplicativo do Windows. Se um modelo com esses metadados for colocado em dois níveis de pasta abaixo do nó de nível superior [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] , o modelo será exibido no nó de nível superior na caixa de diálogo **novo projeto** . Se o `NumberOfParentCategoriesToRollUp` não estiver definido, o modelo aparecerá apenas no nó no qual ele está localizado fisicamente.

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <NumberOfParentCategoriesToRollUp>2</NumberOfParentCategoriesToRollUp>
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
