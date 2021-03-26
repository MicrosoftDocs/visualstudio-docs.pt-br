---
title: Elemento References (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento References e como ele agrupa as referências de assembly que o modelo adiciona aos projetos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#References
helpviewer_keywords:
- <References> element [Visual Studio Templates]
- References element [Visual Studio Templates]
ms.assetid: 1969146d-46bf-422d-8d46-0e9493925003
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: be367bbd1b466c5df3051af384ccefdcf93f8b44
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056565"
---
# <a name="references-element-visual-studio-templates"></a>Elemento References (modelos do Visual Studio)
Agrupa as referências de assembly que o modelo adiciona aos projetos.

 \<VSTemplate> \<TemplateContent>
 \<References>

## <a name="syntax"></a>Sintaxe

```xml
<References>
    <Reference>... </Reference>
    <Reference>... </Reference>
    ...
</References>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos
 Nenhum.

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Referência](../extensibility/reference-element-visual-studio-templates.md)|Elemento necessário.<br /><br /> Especifica a referência de assembly a ser adicionada quando o item for adicionado a um projeto. Deve haver um ou mais `Reference` elementos em um `References` elemento.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|Especifica o conteúdo do modelo.|

## <a name="remarks"></a>Comentários
 `References` é um elemento filho opcional de `TemplateContent` .

 Os `Reference` `References` elementos e só podem ser usados em arquivos *. vstemplate* que tenham um `Type` valor de atributo de `Item` .

## <a name="example"></a>Exemplo
 O exemplo a seguir ilustra o `TemplateContent` elemento de um modelo de item. Esse XML adiciona referências aos assemblies *System.dll* e *System.Data.dll* .

```xml
<TemplateContent>
    <References>
        <Reference>
            <Assembly>
                System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
            </Assembly>
        </Reference>
        <Reference>
            <Assembly>
                System.Data, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
            </Assembly>
        </Reference>
    </References>
    ...
</TemplateContent>
```

## <a name="see-also"></a>Confira também
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)
