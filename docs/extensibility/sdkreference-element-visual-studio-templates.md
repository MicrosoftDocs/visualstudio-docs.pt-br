---
title: Elemento SDKReference (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento SDKReference e como ele especifica que o modelo de item usa uma referência de SDK.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 72c8b352-0b7a-42b3-ba5d-2a2d1e90c34b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5ea070cf466782a1da09e1ba48d08a6965fd041a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063702"
---
# <a name="sdkreference-element-visual-studio-templates"></a>Elemento SDKReference (Modelos do Visual Studio)
Especifica que o modelo de item usa uma referência de SDK.

## <a name="syntax"></a>Sintaxe

```xml
<VSTemplate>
    <TemplateContent>
        <References>
            <Reference>
                <SDKReference>SDKname</SDKReference>
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

## <a name="remarks"></a>Comentários
 Esse texto especifica a referência do SDK a ser adicionada a um projeto quando o modelo de item é instanciado.

```xml
<VSTemplate Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">
    <TemplateData> . . . </TemplateData>
    <TemplateContent>
        <References>
            <Reference>
                <SDKReference>Microsoft Visual C++ Runtime Package, Version=11.0.0.0</SDKReference>
...
```

## <a name="see-also"></a>Confira também
- [Elemento References (Modelos do Visual Studio)](../extensibility/references-element-visual-studio-templates.md)
- [Elemento Reference (Modelos do Visual Studio)](../extensibility/reference-element-visual-studio-templates.md)
- [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Referência de esquema do modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
