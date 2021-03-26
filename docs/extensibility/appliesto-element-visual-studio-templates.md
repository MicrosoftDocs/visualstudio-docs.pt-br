---
title: Elemento AppliesTo (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento AppliesTo e como ele especifica uma expressão opcional para corresponder a um ou mais recursos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 8fb1334b-d78c-405f-98b4-786e9f6b58d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 340ac4db04b62abade9c6572335e28c9fb27b495
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097468"
---
# <a name="appliesto-element-visual-studio-templates"></a>Elemento AppliesTo (modelos do Visual Studio)

Especifica uma expressão opcional para corresponder a um ou mais recursos (consulte <xref:Microsoft.VisualStudio.Shell.Interop.VsProjectCapabilityExpressionMatcher> ). Os recursos são expostos por tipos de projeto por meio da hierarquia como uma __VSHPROPID5 de propriedade [. VSHPROPID_ProjectCapabilities](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID5.VSHPROPID_ProjectCapabilities>). Dessa maneira, o modelo pode ser compartilhado por vários tipos de projeto que têm recursos aplicáveis comuns.

Esse elemento é opcional. Pode haver um máximo de uma instância em um arquivo de modelo. Esse elemento permite que apenas um modelo de item seja aceito como aplicável, com base nos recursos do projeto ativo atualmente selecionado. Ele não pode ser usado para tornar um modelo de item não aplicável. Se `AppliesTo` estiver ausente ou a expressão não for aceita com sucesso, `TemplateID` ou `TemplateGroupID` serão usados para tornar o modelo aplicável, como nas versões anteriores do produto.

Introduzido no Visual Studio 2013 Atualização 2. Para fazer referência à versão correta, consulte fazendo referência a [assemblies entregues na atualização 2 do SDK do Visual Studio 2013](/previous-versions/dn632168(v=vs.120)).

```xml
<VSTemplate>
   <TemplateData>
      <AppliesTo>
```

## <a name="syntax"></a>Sintaxe

```xml
<AppliesTo>Capability1</AppliesTo>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Categoriza o modelo.|

## <a name="text-value"></a>Valor de texto

Um valor de texto é obrigatório. Esse texto especifica os recursos do projeto.

A sintaxe da expressão válida é definida como:

- A expressão de funcionalidade, como "(Visual c++ &#124; CSharp) + (MSTest &#124; NUnit)".

- O "&#124;" é o operador OR.

- Os caracteres "&" e "+" são ambos e operadores.

- O caractere "!" é o operador NOT.

- Parênteses forçam a ordem de precedência de avaliação.

- Uma expressão nula ou vazia é avaliada como uma correspondência.

- Os recursos do projeto podem ser qualquer caractere, exceto estes caracteres reservados: "' ':;, +-*/ \\ ! ~&#124;&% $ @ ^ () = {} [] <>? \t\b\n\r

## <a name="example"></a>Exemplo

O exemplo a seguir mostra três modelos diferentes. `Template1` aplica-se a todos os tipos de projeto C# ou qualquer outro tipo de projeto que ofereça suporte à `WindowsAppContainer` funcionalidade. `Template2` aplica-se a todos os projetos C# de qualquer tipo. `Template3` aplica-se a projetos C# que não são `WindowsAppContainer` projetos.

```xml
<!--  Template 1 -->
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <AppliesTo>CSharp | WindowsAppContainer</AppliesTo>
    </TemplateData>
</VSTemplate>

<!--  Template 2 -->
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <AppliesTo>CSharp</AppliesTo>
    </TemplateData>
</VSTemplate>

<!--  Template 1 -->
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <AppliesTo>CSharp_Class + (!WindowsAppContainer)</AppliesTo>
    </TemplateData>
</VSTemplate>
```

## <a name="see-also"></a>Confira também

- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
