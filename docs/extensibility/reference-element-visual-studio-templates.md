---
title: Elemento Reference (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento Reference e como ele especifica a referência de assembly a ser adicionada quando o item for adicionado a um projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Reference
helpviewer_keywords:
- Reference element [Visual Studio templates]
- <Reference> element [Visual Studio templates]
ms.assetid: 852772ea-c324-42e9-8c8a-6d565414a109
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6fc23edf0897ca71f1b59f126987e42f9d3cb1a8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068512"
---
# <a name="reference-element-visual-studio-templates"></a>Elemento Reference (modelos do Visual Studio)
Especifica a referência de assembly a ser adicionada quando o item for adicionado a um projeto.

 \<VSTemplate> \<TemplateContent>
 \<References>
 \<Reference>

## <a name="syntax"></a>Sintaxe

```xml
<Reference>
    <Assembly> ... </Assembly>
</Reference>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos
 Nenhum.

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Assembly](../extensibility/assembly-element-visual-studio-templates.md)|Elemento necessário.<br /><br /> Especifica informações sobre um assembly, que o modelo usa para adicionar uma referência desse assembly a projetos. Deve haver um `Assembly` elemento em todos os `Reference` elementos.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Referências](../extensibility/references-element-visual-studio-templates.md)|Agrupa as referências de assembly que o modelo adiciona aos projetos.|

## <a name="remarks"></a>Comentários
 `Reference` é um elemento filho obrigatório de `References` .

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
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
