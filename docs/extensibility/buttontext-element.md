---
title: Elemento ButtonText | Microsoft Docs
description: O elemento ButtonText permite especificar o texto que aparece em vários menus. O elemento ButtonText não poderá ficar em branco mesmo que outros campos de texto sejam especificados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- ButtonText element (VSCT XML schema)
- VSCT XML schema elements, ButtonText
ms.assetid: 56aba884-0356-4894-ae4e-32d3938f6865
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cf20a6876dd7ba52413a11f30a3d0130b32e535d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900702"
---
# <a name="buttontext-element"></a>Elemento ButtonText
Esse campo permite especificar o texto que aparece em vários menus. Por padrão, o `ButtonText` elemento aparece nos controladores de menu. O `ButtonText` elemento também se tornará o padrão se os outros campos de texto estão em branco. O `ButtonText` elemento não poderá ficar em branco mesmo que os outros campos de texto sejam especificados.

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
|[Elemento Strings](../extensibility/strings-element.md)|Grupos de elementos de texto, como `ButtonText` e `CommandName` .|

## <a name="text-value"></a>Valor de texto
 O valor de texto do elemento fornece o texto exibido para itens de menu, combinaçãos e outros elementos de interface do usuário que têm `ButtonText` texto visível.

## <a name="see-also"></a>Confira também
- [Visual Studio de tabela de comandos (.vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
