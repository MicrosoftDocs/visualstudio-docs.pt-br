---
title: Elemento GuidSymbol | Microsoft Docs
description: O elemento GuidSymbol contém o GUID do par GUID:ID que representa um menu, grupo ou comando.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, GuidSymbol
- GuidSymbol element (VSCT XML schema)
ms.assetid: 11fb3545-8974-4776-9a54-6b6e7739ae31
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7c30c7a48b03b5deed3267e106e926d3cb5114c1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902755"
---
# <a name="guidsymbol-element"></a>Elemento GuidSymbol
O `GuidSymbol` elemento contém o GUID do par GUID:ID que representa um menu, grupo ou comando. A ID vem de `IDSymbol` um elemento no elemento `GuidSymbol` . O `GuidSymbol` elemento tem um atributo que fornece um nome amigável para o `name` GUID, que está contido no atributo `value` .

## <a name="syntax"></a>Sintaxe

```xml
<GuidSymbol name="guidMyCommandSet" value="{xxxxxxxxxxxxx-xxxx-xxxx-xxxxxxxxxxxx}">
  <IDSymbol>... </IDSymbol>
  <IDSymbol>... </IDSymbol>
</GuidSymbol>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|name|Obrigatórios. Nome do símbolo GUID.|
|value|Obrigatórios. GUID do símbolo guid.|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento IDSymbol](../extensibility/idsymbol-element.md)|Contém a ID do par GUID:ID que representa um menu, grupo ou comando.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento Symbols](../extensibility/symbols-element.md)|Grupos `GuidSymbol` de elementos em um arquivo *.vsct.*|

## <a name="remarks"></a>Comentários
 Normalmente, um arquivo *.vsct* contém três elementos em sua seção, um para o próprio pacote, um para o conjunto de comandos (a coleção de menus, grupos e comandos que o pacote disponibiliza) e outro para os bitmaps que fornecem ícones para botões e outros `GuidSymbol` `Symbols` componentes visuais. Cada `IDSymbol` elemento em um determinado elemento deve ter um `GuidSymbol` `value` exclusivo. No entanto, `IDSymbol` elementos que têm valores idênticos podem existir em um pacote, desde que tenham pais diferentes.

## <a name="see-also"></a>Confira também
- [Visual Studio de tabela de comandos (.vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
