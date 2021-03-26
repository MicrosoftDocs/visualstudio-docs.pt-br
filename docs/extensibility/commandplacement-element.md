---
title: Elemento CommandPlacement | Microsoft Docs
description: O elemento CommandPlacement permite que os botões, grupos e menus sejam incluídos em mais de um grupo ou menu.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CommandPlacements element (VSCT XML schema)
- VSCT XML schema elements, CommandPlacements
ms.assetid: 2cbd7ac8-c55a-43d8-a26d-713b3d790016
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 73d97e32314de0b01bf26025c1fee412de7d9795
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089609"
---
# <a name="commandplacement-element"></a>Elemento CommandPlacement
O elemento CommandPlacement permite que os botões, grupos e menus sejam incluídos em mais de um grupo ou menu. Usando o elemento CommandPlacement, você não precisa redefinir completamente esses itens para modificar a aparência de uma interface do usuário.

 Para obter mais informações, consulte [criar grupos de botões reutilizáveis](../extensibility/creating-reusable-groups-of-buttons.md).

## <a name="syntax"></a>Sintaxe

```
<CommandPlacement guid="guidMyCommandSet" id="MyCommand" priority="0x001" >
  <Parent>... </Parent>
</CommandPlacement>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|guid|Obrigatórios. O GUID do conjunto de comandos, conforme definido no [elemento Symbols](../extensibility/symbols-element.md).|
|id|Obrigatórios. A ID do menu, do grupo ou do comando a ser colocado, conforme definido no `Symbols Element` .|
|priority|Obrigatórios. Determina a posição visual do item em seu elemento pai.|
|Condição|Opcional. Consulte [Aattributes condicional](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|Pai|Obrigatórios. O menu ou grupo que hospeda o item a ser colocado.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento CommandPlacements](../extensibility/commandplacements-element.md)|Especifica grupos de elementos CommandPlacements e CommandPlacement.|

## <a name="example"></a>Exemplo

```
<CommandPlacements>
  <CommandPlacement guid="guidWidgetPackage" id="cmdidInsertOptions"
    priority="0x0300">
    <Parent guid="cmdGuidWidgetCommands" id="menuIDEditWidget"/>
  </CommandPlacement>
</CommandPlacements>
```

## <a name="see-also"></a>Confira também
- [Elemento CommandPlacements](../extensibility/commandplacements-element.md)
- [Arquivos de tabela de comando do Visual Studio (. vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
