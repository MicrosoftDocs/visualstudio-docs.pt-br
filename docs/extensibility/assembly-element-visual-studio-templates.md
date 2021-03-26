---
title: Elemento assembly (modelos do Visual Studio) | Microsoft Docs
titleSuffix: ''
description: Saiba mais sobre o elemento assembly e como ele especifica informações sobre um assembly, que o modelo usa para adicionar uma referência desse assembly aos projetos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Assembly
helpviewer_keywords:
- Assembly element [Visual Studio templates]
- <Assembly> element [Visual Studio templates]
ms.assetid: 9242f76a-1273-4b8a-8f26-6606f91829ef
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 54fc5cfccde99776136f0cb904d02bf6a4971045
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097312"
---
# <a name="assembly-element-visual-studio-templates"></a>Elemento assembly (modelos do Visual Studio)
Especifica informações sobre um assembly, que o modelo usa para adicionar uma referência desse assembly a projetos.

 \<VSTemplate> \<TemplateContent>
 \<References>
 \<Reference>
 \<Assembly>

## <a name="syntax"></a>Sintaxe

```
<Assembly> AssemblyName </Assembly>
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
|[Referência](../extensibility/reference-element-visual-studio-templates.md)|Especifica a referência de assembly a ser adicionada quando o item for adicionado a um projeto.|

## <a name="text-value"></a>Valor de texto
 Um valor de texto é obrigatório.

 Esse texto especifica o assembly a ser adicionado a um projeto quando o modelo de item é instanciado. Esse nome de assembly deve ser especificado de uma das seguintes maneiras:

- Como um nome de assembly completo. Por exemplo:

    ```
    <Assembly>
        MyAssembly, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, Custom = null.
    </Assembly>
    ```

- Como referência de texto simples. Por exemplo:

    ```
    <Assembly> System </Assembly>
    ```

## <a name="remarks"></a>Comentários
 `Assembly` é um elemento filho obrigatório de `Reference` .

 Os `Reference` `References,` elementos e `Assembly` podem ser usados somente em arquivos *. vstemplate* que tenham um `Type` valor de atributo de `Item` .

## <a name="example"></a>Exemplo
 O exemplo a seguir ilustra o `TemplateContent` elemento de um modelo de item. Esse XML adiciona referências aos assemblies *System.dll* e *System.Data.dll* .

```
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
