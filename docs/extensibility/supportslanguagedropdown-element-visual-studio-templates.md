---
title: Elemento SupportsLanguageDropDown (modelos do Visual Studio)
titleSuffix: ''
description: Saiba mais sobre o elemento SupportsLanguageDropDown e como ele especifica se o modelo de item da Web é idêntico para vários idiomas e se a opção Language está habilitada.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SupportsLanguageDropDown
helpviewer_keywords:
- SupportsLanguageDropDown element [Visual Studio Templates]
- <SupportsLanguageDropDown> element [Visual Studio Templates]
ms.assetid: 641197d5-f724-4c06-bc47-2e22dad3fbfb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 67bf92c8c447faac2969bde3f208823158663712
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056071"
---
# <a name="supportslanguagedropdown-element-visual-studio-templates"></a>Elemento SupportsLanguageDropDown (modelos do Visual Studio)

Especifica se o modelo de item da Web é idêntico a vários idiomas e se a opção **idioma** está habilitada na caixa de diálogo **Adicionar novo item** .

 \<VSTemplate> \<TemplateData>
 \<SupportsLanguageDropDown>

## <a name="syntax"></a>Sintaxe

```xml
<SupportsLanguageDropDown> true/false </SupportsLanguageDropDown>
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

 O texto deve ser `true` ou `false` , indicando se a opção de **idioma** está disponível ou não na caixa de diálogo **Adicionar novo item** .

## <a name="remarks"></a>Comentários

 `SupportsLanguageDropDown` é um elemento opcional. O valor padrão é `false`.

 O `SupportsLanguageDropDown` elemento só está disponível para modelos de item da Web.

 Se o valor desse elemento for definido como `true` , o modelo de item será idêntico para todas as linguagens de programação e a opção **idioma** será habilitada na caixa de diálogo **Adicionar novo item** . Essa opção permite que você escolha a linguagem de programação do novo item que você deseja criar a partir do modelo.

## <a name="example"></a>Exemplo

 O exemplo a seguir especifica a exibição da opção de menu suspenso **Language** .

```xml
<VSTemplate Version="3.0.0" Type="Project"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">>
    <TemplateData>
        <Name>MyWebProjecStarterKit</Name>
        <Description>A simple Web template</Description>
        <Icon>icon.ico</Icon>
        <ProjectType>Web</ProjectType>
        <ProjectSubType>CSharp</ProjectSubType>
        <DefaultName>WebSite</DefaultName>
        <SupportsLanguageDropDown>true</SupportsLanguageDropDown>
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
