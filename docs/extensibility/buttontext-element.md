---
title: Elemento ButtonText | Microsoft Docs
description: O elemento ButtonText permite especificar o texto que aparece em vários menus. O elemento ButtonText não pode ficar em branco mesmo que outros campos de texto sejam especificados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ButtonText element (VSCT XML schema)
- VSCT XML schema elements, ButtonText
ms.assetid: 56aba884-0356-4894-ae4e-32d3938f6865
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4fa9ad6aab9d42113f3e01760e191184e168b62d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068109"
---
# <a name="buttontext-element"></a>Elemento ButtonText
Esse campo permite que você especifique o texto que aparece em vários menus. Por padrão, o `ButtonText` elemento aparece em controladores de menu. O `ButtonText` elemento também se tornará o padrão se os outros campos de texto estiverem em branco. O `ButtonText` elemento não pode ficar em branco mesmo que os outros campos de texto sejam especificados.

## <a name="syntax"></a>Sintaxe

```xml
<ButtonText>My Command</ButtonText>
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
|[Elemento Strings](../extensibility/strings-element.md)|Agrupa elementos de texto, como `ButtonText` e `CommandName` .|

## <a name="text-value"></a>Valor de texto
 O valor de texto do `ButtonText` elemento fornece o texto que é exibido para itens de menu, combinações e outros elementos de interface do usuário que têm texto visível.

## <a name="see-also"></a>Confira também
- [Arquivos de tabela de comando do Visual Studio (. vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
