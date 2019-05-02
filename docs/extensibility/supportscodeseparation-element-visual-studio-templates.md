---
title: Elemento SupportsCodeSeparation (modelos do Visual Studio) | Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SupportsCodeSeparation
helpviewer_keywords:
- SupportsCodeSeparation element [Visual Studio Templates]
- <SupportsCodeSeparation> element [Visual Studio Templates]
ms.assetid: 8112aac8-a269-40e5-b92b-9b9a6ff5a542
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 504e176973cd9bb6f0041254e0de19d675be05df
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62432311"
---
# <a name="supportscodeseparation-element-visual-studio-templates"></a>Elemento SupportsCodeSeparation (modelos do Visual Studio)
Especifica se ou não a **colocar código em arquivo separado** caixa de seleção está habilitada no **Adicionar Novo Item** caixa de diálogo.

 \<VSTemplate > \<TemplateData > \<SupportsCodeSeparation >

## <a name="syntax"></a>Sintaxe

```
<SupportsCodeSeparation> true/false </SupportsCodeSeparation>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Elemento obrigatório.<br /><br /> Categoriza o modelo e define como ele é exibido em qualquer um de **novo projeto** ou o **Novo Item** caixa de diálogo.|

## <a name="text-value"></a>Valor de texto
 Um valor de texto é obrigatório.

 O texto deve ser `true` ou `false`, indicando ou não a **colocar código em arquivo separado** caixa de seleção está habilitada no **Add New Item** caixa de diálogo.

## <a name="remarks"></a>Comentários
 `SupportsCodeSeparation` é um elemento opcional. O valor padrão é `false`.

 O `SupportsCodeSeparation` elemento só está disponível para modelos de item da Web.

 Separação de código ou o modelo de página code-behind, permite que você mantenha a marcação em um arquivo e o código de programação em outro arquivo. [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] e outras linguagens .NET usam esse modelo.

## <a name="example"></a>Exemplo
 O exemplo a seguir especifica que o **colocar código em arquivo separado** opção.

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

## <a name="see-also"></a>Consulte também
- [Referência de esquema do modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)