---
title: Incluir elemento | Microsoft Docs
description: O elemento Include especifica um arquivo que pode ser localizado no caminho de inclusão fornecido para inserção no arquivo atual.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- Include
helpviewer_keywords:
- Include element (VSCT XML schema)
- VSCT XML schema elements, Include
ms.assetid: c923dfe6-084a-4105-aec1-f0a3f8399c54
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d0005626c7fbb276775661a7cfb73d17f5e20d62
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899349"
---
# <a name="include-element"></a>Elemento Include
O elemento Include especifica um arquivo que pode ser localizado no caminho de inclusão fornecido para inserção no arquivo atual.  Todos os símbolos e tipos definidos se tornarão parte do resultado compilado.

## <a name="syntax"></a>Sintaxe

```csharp
<Include href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|href|Obrigatórios. O caminho para o arquivo de header:<br /><br /> href="stdidcmd.h"|
|Condição|Opcional. Consulte [Atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|Nenhum.|Nenhum.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento CommandTable](../extensibility/commandtable-element.md)|Define todos os elementos que representam comandos – ou seja, itens de menu, menus, barras de ferramentas e caixas de combinação – que um VSPackage fornece ao IDE.|

## <a name="example"></a>Exemplo

```
<Include href="PackagePlacements.vsct"/>
```

## <a name="see-also"></a>Confira também
- [Visual Studio de tabela de comandos (.vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
