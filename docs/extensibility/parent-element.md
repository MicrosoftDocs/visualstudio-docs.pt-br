---
title: Elemento pai | Microsoft Docs
description: O elemento pai especifica que um elemento é um pai de um botão, caixa de combinação, menu ou grupo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Parent
- Parent element (VSCT XML schema)
ms.assetid: e4624ac8-1b9a-4940-910a-528a661cefad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2ac914fd3245982af89facb97ff2d528b410da99
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090376"
---
# <a name="parent-element"></a>Elemento pai
O pai de um botão ou caixa de combinação pode ser apenas um grupo. O pai de um menu ou grupo pode ser qualquer outro menu ou grupo. Em um [elemento CommandPlacement](../extensibility/commandplacement-element.md), esse elemento é necessário; em todas as outras instâncias, é opcional. Se esse elemento for omitido, o pai de `Group_Undefined:0` será implícito.

## <a name="syntax"></a>Sintaxe

```xml
<Parent guid="guidMyCommandSet" id="MyParentGroupOrMenu" />
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|guid|Obrigatórios. GUID do identificador de comando de GUID/ID.|
|id|Obrigatórios. ID do identificador de comando de GUID/ID.|

### <a name="child-elements"></a>Elementos filho
 Nenhum

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento commandtable](../extensibility/commandtable-element.md)|Define todos os elementos que representam comandos que um VSPackage fornece ao IDE (ambiente de desenvolvimento integrado). Por exemplo, itens de menu, menus, barras de ferramentas e caixas de combinação.|
|[Elemento Buttons](../extensibility/buttons-element.md)|Elementos do [elemento Button](../extensibility/button-element.md) de groups.|
|[Elemento menus](../extensibility/menus-element.md)|Define todos os menus que um VSPackage implementa.|
|[Elemento groups](../extensibility/groups-element.md)|Contém entradas que definem os grupos de comandos de um VSPackage.|

## <a name="see-also"></a>Confira também
- [Arquivos de tabela de comando do Visual Studio (. vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
