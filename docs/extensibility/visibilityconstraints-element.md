---
title: Elemento VisibilityConstraints | Microsoft Docs
description: O elemento VisibilityConstraints determina a visibilidade estática de grupos de comandos e barras de ferramentas.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VisibilityConstraints
helpviewer_keywords:
- VSCT XML schema elements, VisibilityConstraints
- VisibilityConstraints element (VSCT XML schema)
ms.assetid: d6dcd314-6fe4-4693-a189-91fa026c7b34
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d97f72e7a29f3cbb23c775df8454952f5ffac928
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062558"
---
# <a name="visibilityconstraints-element"></a>Elemento VisibilityConstraints
O elemento VisibilityConstraints determina a visibilidade estática de grupos de comandos e barras de ferramentas. A visibilidade é primeiro controlada pelo [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE (ambiente de desenvolvimento integrado) sem carregar o VSPackage.

## <a name="syntax"></a>Sintaxe

```xml
<VisibilityConstraints>
  <VisibilityItem />
  <VisibilityItem />
</VisibilityConstraints>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|Condição|Opcional. Consulte [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento VisibilityItem](../extensibility/visibilityitem-element.md)|Determina a visibilidade estática de comandos e barras de ferramentas.|
|[VisibilityConstraints](../extensibility/visibilityconstraints-element.md)|Determina a visibilidade estática de grupos de comandos e barras de ferramentas.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento commandtable](../extensibility/commandtable-element.md)|Define todos os elementos que representam os comandos (por exemplo, itens de menu, menus, barras de ferramentas e caixas de combinação) que um VSPackage fornece ao IDE.|

## <a name="example"></a>Exemplo

```xml
<VisibilityConstraints>
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"
    context="guidNotViewSourceMode"/>
</VisibilityConstraints>
```

## <a name="see-also"></a>Confira também
- [Elemento VisibilityItem](../extensibility/visibilityitem-element.md)
- [Tabela de comandos do Visual Studio (. Arquivos de vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
