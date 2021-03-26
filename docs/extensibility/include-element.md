---
title: Elemento include | Microsoft Docs
description: O elemento include especifica um arquivo que pode estar localizado no caminho de inclusão fornecido para inserção no arquivo atual.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: fd64f897dc2a089a2e94f5e0c53e3ef116f7b385
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082095"
---
# <a name="include-element"></a>Elemento include
O elemento include especifica um arquivo que pode estar localizado no caminho de inclusão fornecido para inserção no arquivo atual.  Todos os símbolos e tipos definidos se tornarão parte do resultado compilado.

## <a name="syntax"></a>Sintaxe

```csharp
<Include href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|href|Obrigatórios. O caminho para o arquivo de cabeçalho:<br /><br /> href = "stdidcmd. h"|
|Condição|Opcional. Consulte [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|Nenhum.|Nenhum.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento commandtable](../extensibility/commandtable-element.md)|Define todos os elementos que representam comandos (ou seja, itens de menu, menus, barras de ferramentas e caixas de combinação) que um VSPackage fornece ao IDE.|

## <a name="example"></a>Exemplo

```
<Include href="PackagePlacements.vsct"/>
```

## <a name="see-also"></a>Confira também
- [Arquivos de tabela de comando do Visual Studio (. vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
