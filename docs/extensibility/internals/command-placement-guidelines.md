---
title: Diretrizes de posicionamento de comando | Microsoft Docs
description: Conheça as diretrizes e as práticas recomendadas para posicionar comandos no IDE (ambiente de desenvolvimento integrado) do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, small command sets
- small command sets
- command sets
ms.assetid: 63b3478e-e08a-420b-a0ec-76767e0cb289
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 46aa6c341313a9d7c9d0a6d1666130d799ddc277
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057319"
---
# <a name="command-placement-guidelines"></a>Diretrizes de posicionamento de comando
As práticas recomendadas para posicionamento de comandos no ambiente de desenvolvimento integrado (IDE) do Visual Studio variam de acordo com o tamanho do conjunto de comandos. Os comandos são definidos e posicionados de acordo com as informações em arquivos *. vsct* .

## <a name="best-practices-for-all-command-sets"></a>Práticas recomendadas para todos os conjuntos de comandos
 Para cada conjunto de comandos, siga estas diretrizes:

- Prepare um gráfico da estrutura de comandos com antecedência. Identifique os comandos, caixas de combinação, grupos de comandos e menus de atalho que serão usados em mais de um local.

- Os comandos que aparecem no mesmo grupo devem estar relacionados.

- Os grupos que contêm apenas um comando são aceitáveis.

- Os pacotes não devem adicionar muitos comandos aos menus existentes do Visual Studio. Em vez disso, eles devem criar menus ou submenus para hospedar os novos comandos.

- Quando você coloca um comando em um menu existente, nomeie o comando para que seu objetivo fique claro e não será confundido com os comandos existentes.

## <a name="best-practices-for-small-command-sets"></a>Práticas recomendadas para conjuntos de comandos pequenos
 Se você estiver desenvolvendo um VSPackage que tenha apenas alguns comandos, também siga estas diretrizes:

- Quando possível, use o elemento [pai](../../extensibility/parent-element.md) de um comando, caixa de combinação, grupo ou menu filho para colocá-lo no grupo apropriado.

- Atribua esses grupos aos menus exibidos pelo VSPackage.

- O pai de um menu filho ou um comando deve ser um elemento de [grupo](../../extensibility/group-element.md) . Atribua comandos e menus filho a grupos e, em seguida, atribua os grupos aos menus pai.

- Você pode colocar um comando em grupos adicionais adicionando uma seção do elemento [CommandPlacements](../../extensibility/commandplacements-element.md) após a definição do comando e, em seguida, adicionando ao `CommandPlacements` elemento um elemento [CommandPlacement](../../extensibility/commandplacement-element.md) para cada grupo adicional.

## <a name="best-practices-for-large-command-sets"></a>Práticas recomendadas para conjuntos de comandos grandes
 Se seu VSPackage terá muitos comandos que aparecerão em vários contextos, também siga estas diretrizes:

- Crie menus, grupos e comandos de auto-Parent. Ou seja, não atribua um `Parent` elemento na definição do item.

- Use `CommandPlacement` entradas de elemento na `CommandPlacements` seção do elemento para colocar menus, grupos e comandos em seus menus e grupos pai.

- Na `CommandPlacements` seção do elemento, as entradas que populam um determinado menu ou grupo devem ser adjacentes umas às outras. Isso ajuda a legibilidade e torna as `Priority` classificações mais fáceis de determinar.

## <a name="see-also"></a>Confira também
- [Como VSPackages adicionar elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Arquivos de tabela de comando do Visual Studio (. vsct)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
